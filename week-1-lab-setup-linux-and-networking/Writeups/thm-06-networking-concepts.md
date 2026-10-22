# TryHackMe: Networking Concepts

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Networking Concepts |
| **Link** | https://tryhackme.com/room/networkingconcepts |
| **Difficulty** | Easy |
| **Date completed** | 19/10/1026 |
| **Status** | Completed |

## Objective
Understand core networking concepts, including the OSI and TCP/IP models, IP addressing and subnetting, TCP and UDP transport protocols, data encapsulation, and the use of Telnet to communicate with remote services.

## Key Concepts
- The seven layers of the OSI model and their functions
- The four layers of the TCP/IP model
- IPv4 addressing, network addresses, host addresses, and subnet masks
- Subnetting and dividing networks into smaller logical networks
- TCP connection-oriented communication and reliable data delivery
- UDP connectionless communication and low-overhead data transmission
- Encapsulation and decapsulation across networking layers
- Telnet as a protocol and command-line client for remote communication
- The security risks of transmitting data over unencrypted protocols

## Tools and Commands Used
- `ipconfig`: Displays IP configuration details on Windows.
- `ip addr`: Displays network interface and IP address information on Linux.
- `ping`: Tests network reachability using ICMP.
- `telnet`: Connects to a remote host and port to interact with a service that supports the relevant protocol.

Example:
```bash
telnet 192.168.1.10 23
```

This attempts to connect to port 23 on the specified host, commonly associated with Telnet.

## Summary
The Networking Concepts room covered the foundational principles behind communication between networked systems. It explored the OSI and TCP/IP models, IP addressing and subnetting, the differences between TCP and UDP, and how encapsulation prepares data for transmission. The Telnet section introduced remote communication with network services and highlighted the security implications of using protocols that transmit information without encryption. These concepts are important for understanding network behaviour, troubleshooting connectivity, and analysing potential security weaknesses.

## Evidence

![THM Room](/Findings/TryHackMe/networking-concepts.png)

## Lessons Learned
- The OSI and TCP/IP models provide frameworks for understanding how data moves between applications and network interfaces.
- IP addresses identify network interfaces logically, while subnet masks determine which addresses belong to a particular network.
- Subnetting helps divide larger networks into smaller networks for improved address management and network segmentation.
- TCP provides reliable, ordered delivery through connection-oriented communication, while UDP offers connectionless delivery without the same built-in reliability guarantees.
- The choice between TCP and UDP depends on an application's requirements for reliability, latency, and overhead.
- Encapsulation adds protocol information as data passes through networking layers, enabling devices to deliver and process it correctly.
- Telnet can be useful for learning how remote services communicate, but it does not encrypt its sessions and should not be used to transmit sensitive credentials over untrusted networks.
- Secure alternatives such as SSH should be preferred for remote command-line administration.
- Understanding ports, protocols, addressing, and network layers supports effective network troubleshooting and cybersecurity reconnaissance.

## How this connects to my Week 1 lab
This supports my notes on ports and protocols, and the `ss -tulpn` output on Ubuntu shows these ports in action.
