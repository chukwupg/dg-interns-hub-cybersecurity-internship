# TryHackMe: What is Networking

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | What is Networking |
| **Link** | https://tryhackme.com/room/whatisnetworking |
| **Difficulty** | Informative |
| **Date completed** | 18/10/2026 |
| **Status** | Completed |

## Objective
Understand the fundamentals of computer networking, how the Internet connects devices worldwide, how devices are identified on a network, and how the `ping` command uses ICMP to test connectivity.

## Key Concepts
- Computer networking and communication between connected devices
- The Internet as a global network of interconnected networks
- IP addresses for identifying devices and enabling network communication
- MAC addresses for identifying network interfaces at the data link layer
- Packets and how data travels across networks
- ICMP (Internet Control Message Protocol)
- `ping` for testing network connectivity and measuring response time
- Introduction to Local Area Networks (LANs)

## Tools and Commands Used
- `ping`: Sends ICMP Echo Requests to test whether a destination is reachable and measures response times.

Example:
```bash
ping 192.168.1.1
```

- **IP addresses:** Used to identify network interfaces logically and route traffic between networks.
- **MAC addresses:** Used to identify interfaces for communication on the local network.
- **ICMP:** A network-layer protocol used for diagnostic messages and connectivity testing.

## Summary
The What is Networking? room introduced the fundamentals of computer networking, the Internet, device identification, and network connectivity testing. It explained how devices communicate through interconnected networks and how IP and MAC addresses serve different purposes in identifying devices and delivering traffic. The room also introduced ICMP and the `ping` command as basic tools for testing connectivity between hosts. The final task provided a pathway to continue learning through the Intro to LAN room, building a foundation for understanding network devices, protocols, and local network communication.

## Evidence

![THM Room](/Findings/TryHackMe/what-is-networking.png)

## Lessons Learned
- Networking enables devices to exchange data and share resources through connected systems.
- The Internet is a global network of interconnected networks that communicate using standard protocols.
- IP addresses provide logical addressing, while MAC addresses identify network interfaces at the data link layer.
- A MAC address can be spoofed.
- Data is transmitted across networks in packets rather than as one uninterrupted stream.
- The `ping` command uses ICMP Echo Requests and Echo Replies to test reachability, although firewalls or network configurations may block responses.
- Response times and packet loss reported by `ping` can help identify potential connectivity or network performance issues.
- A LAN connects devices within a limited geographical area, such as a home, office, or laboratory.
- Understanding networking fundamentals is essential for cybersecurity tasks such as reconnaissance, traffic analysis, troubleshooting, and network security assessments.

## How this connects to my Week 1 lab
I recorded the IP and MAC addresses of my three VMs and confirmed connectivity with `ping`, which is exactly what this room explains.
