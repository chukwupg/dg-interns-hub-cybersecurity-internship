# DG Interns Hub: Week 1

## Lab Setup, Linux and Networking Foundations
**Intern:** Chukwu PraiseGod 

**Submission date:** 22 October 2026

## Summary
I built an isolated three-VM home lab in VirtualBox, practised Linux administration, mapped the lab network, completed OverTheWire Bandit levels 0 to 10 and eight TryHackMe rooms, and wrote eight theory notes plus a Linux cheat sheet. 

## Folder structure
```
DG Interns Hub
|-- Week 1
    |-- Notes                           (8 theory notes)
    |-- Writeups                        (8 TryHackMe rooms + Bandit levels 0-10)
    |-- Findings
    |   |-- Lab Setup                   (VM list, IPs, pings, snapshots)
    |   |-- Linux Practice              (users, groups, permissions, commands, cron job)
    |   |-- Network Map and Diagram     (draw.io lab diagram)
    |   |-- Over the Wire Bandit        (a screenshot per level)
    |-- Cheat Sheet                     (Linux Command - What It Does - When to Use It)
    |-- Week 1 Report.pdf
    |-- Week 1 Presentation.pptx
    |-- README.md
```

## 1. Lab setup
| VM | Memory | IP address | DNS |
|---|---|---|---|
| Ubuntu | 2 GB | 192.168.98.129 | 192.168.98.1 |
| Kali Linux | 2 GB | 192.168.98.130 | 192.168.98.1 |
| Windows 10 | 4 GB | 192.168.98.131 | 192.168.98.1 |

- Network: isolated, 192.168.98.0/24.
- Pings confirmed between the VMs and a clean snapshot taken of each.
- Evidence: [Findings/Lab Setup](/Findings/Lab%20Setup/).

## 2. Linux practice (Ubuntu)
- 3 users (alice, john, carol) and 2 groups (developers, analysts).
- Shared folder `/srv/shared`, owned by `root:developers`, `chmod 3770`. carol, who is not in the group, got Permission denied.
- Used `find`, `grep`, `ps`, `ss -tulpn` and a cron job; 33+ commands documented with output.
- Evidence: [Findings/Linux Practice](/Findings/Linux%20Practice/).

## 3. Network map
- IP, gateway and DNS recorded for each VM with `ip a`, `ip route`, `ping`, `traceroute`, `nslookup` and `dig`.
- On Ubuntu, `ss -tulpn` showed SSH (22) and mDNS (5353) reachable from the network; DNS (53), printing (631) and time sync (323) on localhost only.
- Diagram: [Findings/Network Map and Diagram](/Findings/Network%20Map%20and%20Diagram/).

## 4. OverTheWire Bandit (levels 0 to 10)
- Completed over SSH with a screenshot and writeup for every level.
- Passwords are not published.
- Writeups: [Writeups](/Writeups/). 
- Screenshots: [Findings/Over the Wire Bandit](/Findings/Over%20the%20Wire%20Bandit/).

## 5. Completed TryHackMe rooms (8)
- Search Skills
- Learning Cyber Security 
- Linux Fundamentals Part 1
- What is Networking
- Introductory Networking
- Networking Concepts
- Pyramid of Pain
- Intro to LAN

Evidence: [TryHackMe](/Findings/TryHackMe/)

## 6. Theory notes 

Read here: [Notes](/Notes/)

| # | Topic |
|---|---|
| 01 | What is cybersecurity and the CIA triad |
| 02 | SOC analyst vs VAPT / penetration tester vs incident responder |
| 03 | OSI vs TCP/IP model, with an attack per layer |
| 04 | IP, MAC, DNS, DHCP, ports and 12 common ports |
| 05 | Linux file system hierarchy and permissions (chmod, chown, SUID) |
| 06 | Threat vs vulnerability vs risk vs exploit |
| 07 | VM networking modes and why vulnerable labs are never bridged |
| 08 | Legal and ethical basics, including Nigeria's Cybercrimes Act |

## 7. Cheat sheet
Built a table containing 30+ commands under three columns 
- Linux Command
- What It Does
- When to Use It  

Find it here: [Cheat Sheet](/Cheat%20Sheet/)

## 8. LinkedIn
- Concept post: "SOC analyst vs penetration tester: what is the difference?" (5 bullet points)
- Weekly post: lab setup screenshot and key learnings
- Link 1: [SOC analyst vs penetration tester: what is the difference?](https://lnkd.in/p/e4nR3qS8)
- Link 2: 

## Lessons Learned
- Isolate vulnerable labs and never bridge them to a real network.
- Permissions are security: one wrong `chmod` can expose or lock a folder.
- Every open port is an attack surface; check with `ss -tulpn` or automated tools when permitted.
- Small tools like `grep`, `sort` and `uniq` are powerful when combined.

## Rules followed
- Free tools only
- No plagiarism
- No Bandit passwords published in writeups (except for proof screenshots)
- Submitted before the deadline.
