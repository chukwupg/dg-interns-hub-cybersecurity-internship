# TryHackMe: Introductory Networking

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Introductory Networking |
| **Link** | https://tryhackme.com/room/introtonetworking |
| **Difficulty** | Easy |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Objective
Understand the fundamental models and processes that govern network communication, including the OSI and TCP/IP models, data encapsulation, and practical networking tools used to test connectivity, trace network routes, and investigate domain registration and DNS records.

## Key Concepts
- The seven layers of the OSI model and their functions
- The TCP/IP model and its role in Internet communication
- Encapsulation and decapsulation as data moves through network layers
- Protocol Data Units (PDUs), including segments, packets, and frames
- ICMP and network connectivity testing
- Traceroute and the path packets take to reach a destination
- WHOIS for retrieving domain registration information
- DNS resolution and the purpose of DNS record types
- `dig` for querying DNS servers and inspecting DNS records

## Tools and Commands Used
- `ping`: Tests network reachability using ICMP Echo Requests and measures response times.

```bash
ping 8.8.8.8
```

- `traceroute`: Identifies the network hops taken by packets towards a destination on Linux.

```bash
traceroute example.com
```

On Windows, the equivalent command is:

```powershell
tracert example.com
```

- `whois`: Retrieves available domain registration and ownership-related information.

```bash
whois example.com
```

- `dig`: Queries DNS servers to retrieve records such as A, AAAA, MX, NS, and TXT records.

```bash
dig example.com
dig example.com A
dig example.com MX
dig example.com NS
dig example.com @1.1.1.1
```

Note: These are representative examples of the tools covered in the room, not a confirmed record of every command I executed.

## Summary
Completed the Introductory Networking room, which explored how network communication works through the OSI and TCP/IP models and how encapsulation prepares data for transmission across networks. The practical section introduced `ping` for connectivity testing, `traceroute` for examining network paths, `whois` for researching domain registration details, and `dig` for querying DNS records. Together, these concepts and tools provide a foundation for understanding network traffic, troubleshooting connectivity problems, and conducting initial reconnaissance during cybersecurity assessments.

## Evidence

![THM Room](/Findings/TryHackMe/introductory-networking.png)

## Lessons Learned
- The OSI model divides network communication into seven layers, making network operations and troubleshooting easier to understand.
- The TCP/IP model describes the protocol suite used for practical communication across modern networks and the Internet.
- Encapsulation adds protocol-specific headers, and sometimes trailers, as data moves down the networking stack. Decapsulation reverses this process at the receiving end.
- Understanding the differences between frames, packets, and segments helps explain how data is transmitted across network layers.
- `ping` helps test reachability and response time, but a failed response does not always mean the destination is offline.
- `traceroute` helps identify intermediate network hops, although routers may filter or deprioritise probe traffic.
- WHOIS can reveal useful domain registration details, but privacy protection and registry policies may limit the information available.
- DNS translates domain names into information used to locate services, and different record types serve different purposes.
- The `dig` command provides detailed DNS query results that can help troubleshoot name resolution and support reconnaissance.
- Combining networking theory with command-line tools improves the ability to investigate connectivity issues and understand a target's network infrastructure.

## How this connects to my Week 1 lab
I used `traceroute`, `nslookup` and `dig` in my network map task, and this room supplies the model behind my OSI vs TCP/IP note.
