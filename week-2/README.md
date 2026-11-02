# DG Interns Hub: Week 2 

## Network Traffic Analysis, Nmap and Windows Logging

**Program:** DG Interns Hub Cybersecurity Internship 

**Intern:** Chukwu PraiseGod 

**Submission date:** 30 October, 2026


## 1. Summary

This week I learned to read what happens on the wire and in Windows logs. I captured traffic between my own virtual machines, scanned them with Nmap and watched what each scan looked like in Wireshark, then generated Windows security events and found them in Event Viewer and PowerShell. I also finished six TryHackMe rooms, wrote eight theory notes and six room writeups, and built two cheat sheets. The SYN-scan pattern I found here is what I will detect with Snort in Week 3.


## 2. Lab setup

Everything ran in VMware Workstation Pro on an 8 GB RAM PC, on an isolated network (192.168.98.0/24). I only tested systems I own. All tools were free.

| Machine | Role | Memory / address |
|---|---|---|
| Kali Linux | Runs ping, curl, nslookup and Nmap | 2 GB, 192.168.98.130 |
| Ubuntu | Apache web server and dnsmasq DNS | 2 GB, 192.168.98.129 |
| Windows 10 | Target for scans and event logging | 4 GB, 192.168.98.131 |


## 3. Work done and findings


### 3.1 Capturing traffic

I installed Apache on Ubuntu (`sudo apt install apache2`). From Kali I ran `ping`, `curl` and `nslookup` while Wireshark captured, and took screenshots of the TCP handshake (SYN, SYN/ACK, ACK), an HTTP GET, a DNS query and an ICMP echo. Captures: `full-traffic-capture.pcapng` and `filtered-traffic.pcapng`.

**DNS problem.** `nslookup` against 192.168.98.1 failed with "connection refused" because nothing in the lab was answering DNS on that address. I installed dnsmasq on Ubuntu to resolve `ubuntu.lab`. systemd-resolved already held port 53 on the loopback addresses, so I made dnsmasq listen only on 192.168.98.129. The lookup then worked and produced a clean DNS capture.

**Evidence folder:** [`wireshark`](/week-2/Findings/wireshark/)

### 3.2 Nmap on my own VMs

I ran `-sn`, `-sS`, `-sV`, `-O` and `-A` against both the Ubuntu and Windows VMs and saved the results with `-oN` and `-oX`. I captured the `-sS` scans (`ubuntu-nmap-scan-traffic.pcapng`, `windows-nmap-scan-traffic.pcapng`) and applied this display filter:

```
tcp.flags.syn==1 && tcp.flags.ack==0
```

This shows the scan clearly: a burst of SYN packets from Kali to many ports in a short time. A SYN scan never completes the handshake, and closed ports answer with RST. One source probing many ports with no real conversation is the pattern a defender should look for.

**Evidence folder:** [`nmap`](/week-2/Findings/nmap/)

### 3.3 Windows events

| Event | Log | How I generated it |
|---|---|---|
| 4625 failed logon | Security | Wrong passwords with `net use` and at the lock screen |
| 4624 successful logon | Security | Signed in again; checked the logon type |
| 4720 new user | Security | `net user` to add a test account |
| 4732 added to Administrators | Security | `net localgroup Administrators` |
| 7045 service installed | System | `sc.exe create`, then `sc.exe delete` |
| 1102 log cleared | Security | `wevtutil cl Security`, done last |

The first 4624 I found was **logon type 5** (service), which is normal background activity. Signing in as the new test user gave **logon type 2** (interactive). The sequence 4720, 4732, then a type 2 logon for the same account is what an analyst would flag: a new account gets admin rights and logs in straight away.

**Evidence folder:** [`windows-events`](/week-2/Findings/windows-events/)

### 3.4 PowerShell hunting

I exported every 4625 event to CSV with `Get-WinEvent -FilterHashtable` and counted failures per account with `Group-Object`:

```
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} |
  Select TimeCreated, Id, @{n='Account';e={$_.Properties[5].Value}} |
  Export-Csv failed-4625.csv -NoTypeInformation
Import-Csv failed-4625.csv | Group-Object Account | Sort Count -Desc
```

| Account | Failed logons |
|---|---|
| fakeadmin | 3 |
| my local account (lock-screen attempts) | 2 |
| testuser1 | 1 |
| testuser2 | 1 |

Counting by account turns a long log into a short list, so a repeated name stands out right away.


## 4. Problems and fixes

| Problem | Cause | Fix |
|---|---|---|
| `nslookup` failed (connection refused) | No DNS server on 192.168.98.1 | Set up dnsmasq on Ubuntu and queried `ubuntu.lab` there |
| dnsmasq would not start | systemd-resolved already used port 53 on loopback | Bound dnsmasq to 192.168.98.129 only |
| `sc create` failed in PowerShell | `sc` is an alias for `Set-Content` | Used `sc.exe` |
| Evidence would disappear | Clearing the Security log removes earlier events | Took screenshots and exported the CSV first, cleared the log last |


## 5. Learning outcomes

I completed six TryHackMe rooms (Nmap, Live Host Discovery, Basic Port Scans, Windows Basics, Windows Fundamentals 1 and 2), eight theory notes, six room writeups and two cheat sheets (20 Wireshark filters and 15 Windows Event IDs).

- A completed handshake means a real connection; a burst of SYNs with no completed handshakes means a probe.
- Reading the error message first saved time: the DNS failure was a missing server, not a broken lookup.
- Logon type matters as much as the event ID: type 5 is noise, while type 2 for a brand-new admin account deserves attention.
- Knowing what is normal in my lab (a baseline) is what makes the odd events easy to spot.

**TryHackMe Evidence Folder:** [`TryHackMe`](/week-2/Findings/TryHackMe/)

## 6. Next steps

In Week 3 I will use Snort to write a rule that detects the SYN-scan pattern I captured here, and look at endpoint activity on the Windows VM.


## 7. Ethics and safety

All scanning and testing was done only on virtual machines I own, in an isolated network. No passwords, flags or room answers are included in this report.
