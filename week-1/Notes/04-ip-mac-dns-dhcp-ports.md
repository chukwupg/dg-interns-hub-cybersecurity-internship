# IP, MAC, DNS, DHCP and Ports

## The five building blocks

| Term | What it is | Key facts | Example |
|---|---|---|---|
| **IP address** | Logical address that identifies a device on a network and lets traffic be routed | IPv4 is 32 bits (e.g. 192.168.56.101); IPv6 is 128 bits. Private ranges: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16. Can change when the network changes | 192.168.98.130 |
| **MAC address** | Hardware address of a network interface, used for local delivery (Layer 2) | 48 bits, written like 08:00:27:ab:cd:ef. The first half identifies the manufacturer. Normally fixed, but can be spoofed | 00:0c:29:0d:fe:f5 |
| **DNS** | Translates names (google.com) into IP addresses | Common records: A (IPv4), AAAA (IPv6), MX (mail), NS (name server), CNAME (alias), TXT (text). Uses port 53 | `nslookup google.com` |
| **DHCP** | Automatically gives devices an IP address, gateway and DNS server | The DORA process: Discover, Offer, Request, Acknowledge. Uses UDP ports 67/68 | My VMs got their addresses from VMware's DHCP |
| **Port** | A number (0 to 65535) that identifies a specific service on a device | Well-known 0 to 1023, registered 1024 to 49151, dynamic 49152 to 65535. IP gets traffic to the machine; the port gets it to the right program | SSH on 22 |

## 12 common ports

| Port | Service | Protocol | Typical risk |
|---|---|---|---|
| **21** | FTP (file transfer) | TCP | Sends credentials in plain text; anonymous login; brute force |
| **22** | SSH (secure remote login) | TCP | Brute force and weak passwords or keys; outdated versions |
| **23** | Telnet (remote login) | TCP | Everything in plain text, including passwords; easily sniffed. Replace with SSH |
| **25** | SMTP (sending email) | TCP | Open relay abuse, spam and phishing, user enumeration |
| **53** | DNS | UDP/TCP | Cache poisoning, DNS amplification DDoS, zone transfer leaks, DNS tunneling |
| **80** | HTTP (web) | TCP | Unencrypted traffic; web app attacks such as SQL injection and XSS |
| **110** | POP3 (receiving email) | TCP | Plain-text credentials and email contents if not wrapped in TLS |
| **143** | IMAP (receiving email) | TCP | Plain-text login unless IMAPS is used; brute force |
| **443** | HTTPS (secure web) | TCP | Encrypted, but the app can still be vulnerable; weak TLS settings or expired certificates |
| **445** | SMB (Windows file sharing) | TCP | Worm and ransomware spread (e.g. EternalBlue); null sessions; credential relay |
| **3306** | MySQL (database) | TCP | Database exposed to the internet; weak or default credentials; data theft |
| **3389** | RDP (Windows remote desktop) | TCP | Brute force, exposed RDP is a top ransomware entry point; BlueKeep-type flaws |

## Key points
- Rule of thumb: only expose the ports you need, and prefer encrypted services (SSH over Telnet, HTTPS over HTTP, SFTP over FTP).
- An **open port is not automatically a vulnerability**, but every open port is attack surface.
- Useful commands: `ip a` (IP and MAC), `nslookup` and `dig` (DNS), `ss -tulpn` (listening ports).

## How this shows up in my lab
- My three VMs share one isolated network, **192.168.98.0/24**.

| VM | OS | IP address | Gateway | DNS |
|---|---|---|---|---|
| Ubuntu | Ubuntu | 192.168.98.129 | 192.168.98.1 | 192.168.98.1 |
| Kali | Kali Linux | 192.168.98.130 | 192.168.98.1 | 192.168.98.1 |
| Windows | Windows 10 | 192.168.98.131 | 192.168.98.1 | 192.168.98.1 |

### On Ubuntu, `ss -tulpn` showed which ports are listening:

| Port | Protocol | Bound to | What it is | Reachable from other VMs? |
|---|---|---|---|---|
| 22 | TCP | 0.0.0.0 and [::] (all interfaces) | SSH | **Yes** |
| 5353 | UDP | 0.0.0.0 and [::] (all interfaces) | mDNS (local name discovery) | **Yes** |
| 53 | TCP/UDP | 127.0.0.53 and 127.0.0.54 | Local DNS resolver | No (localhost only) |
| 631 | TCP | 127.0.0.1 and [::1] | CUPS printing service | No (localhost only) |
| 323 | UDP | 127.0.0.1 and [::1] | Time sync service (likely chrony) | No (localhost only) |

- **What I learned:** a service bound to `127.0.0.1` can only be used from the machine itself, while `0.0.0.0` means every network interface. Only SSH (22) and mDNS (5353) can be reached from the other VMs, which keeps the attack surface small.

### Evidence 

![ss -tulnp ouput](/Findings/Linux%20Practice/ss-command-output.png)