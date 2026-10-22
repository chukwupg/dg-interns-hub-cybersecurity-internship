# OSI Model vs TCP/IP Model

## The two models side by side

| | **OSI model** | **TCP/IP model** |
|---|---|---|
| Layers | 7 | 4 |
| Purpose | A reference model for understanding and teaching networking | The practical model the internet actually runs on |
| Layers (top to bottom) | Application, Presentation, Session, Transport, Network, Data Link, Physical | Application, Transport, Internet, Network Access |
| How they map | Layers 5 to 7 - Application, Layer 4 - Transport, Layer 3 - Internet, Layers 1 and 2 - Network Access |

## OSI layers, protocols and one attack per layer

| # | OSI layer | What it does | Example protocols / items | Data unit | TCP/IP layer | Example attack |
|---|---|---|---|---|---|---|
| 7 | **Application** | Services the user's software talks to | HTTP, HTTPS, FTP, SMTP, DNS, SSH | Data | Application | **SQL injection** or XSS against a web app |
| 6 | **Presentation** | Formats, encodes, encrypts and compresses data | TLS/SSL, JPEG, ASCII | Data | Application | **SSL stripping / TLS downgrade** forces a victim onto weaker or no encryption |
| 5 | **Session** | Opens, maintains and closes sessions | NetBIOS, RPC, session tokens | Data | Application | **Session hijacking** by stealing a session cookie |
| 4 | **Transport** | End-to-end delivery, ports, reliability | TCP, UDP | Segment (TCP) / Datagram (UDP) | Transport | **SYN flood** exhausts a server's connection table |
| 3 | **Network** | Logical addressing and routing | IP, ICMP, IPsec | Packet | Internet | **IP spoofing** or ICMP flood |
| 2 | **Data Link** | Local delivery using MAC addresses | Ethernet, ARP, Wi-Fi (802.11) | Frame | Network Access | **ARP spoofing / poisoning**, **Mac spoofing** to intercept or impersonate devices/local traffic |
| 1 | **Physical** | Raw bits over cable, fiber or radio | Cables, hubs, Wi-Fi radio | Bits | Network Access | **Cable tapping** or Wi-Fi jamming |

## Key points
- **Encapsulation:** going down the layers, each layer wraps the data in its own header (data - segment - packet - frame - bits). The receiver reverses this (de-encapsulation).
- **Memory aid (top to bottom):** *All People Seem To Need Data Processing.*
- **Troubleshooting tip:** work bottom-up. Is the cable or Wi-Fi connected (L1)? Does it have an IP (L3)? Is the port open (L4)?
- Attackers target every layer, so defence needs to be layered too (firewalls, encryption, patching, monitoring).

##  How this shows up in my lab
- `ping` between my VMs tests Layer 3 (ICMP). 
- `ss -tulpn` shows Layer 4 ports. 
- `ip neigh` shows Layer 2 MAC-to-IP mappings.
