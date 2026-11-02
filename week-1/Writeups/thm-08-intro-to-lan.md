# TryHackMe: Intro to LAN

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Intro to LAN |
| **Link** | https://tryhackme.com/room/introtolan |
| **Difficulty** | Easy |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Objective
Understand how Local Area Networks (LANs) are structured, how subnetting divides networks into smaller segments, and how ARP and DHCP enable devices to communicate and obtain network configuration automatically.

## Key Concepts
- LAN topologies, including star, bus, and ring
- Physical and logical network layouts 
- IPv4 addressing and subnet masks
- Network addresses, host addresses, and subnetting
- Address Resolution Protocol (ARP)
- Mapping IPv4 addresses to MAC addresses on a local network
- Dynamic Host Configuration Protocol (DHCP)

## Tools and Commands Used
```
Conceptual Room
```

## Summary
The Intro to LAN room introduced how devices are organised and communicate within a Local Area Network. It covered LAN topologies, subnetting, ARP, and DHCP. Topologies describe how network devices are connected, while subnetting divides an IP address range into smaller networks. ARP enables a device to discover the MAC address associated with an IPv4 address on its local network, and DHCP automatically provides devices with IP addresses and other essential network settings. The room also pointed towards the OSI Model as a next step in understanding how network communication operates across different layers.

## Evidence

![THM Room](/Findings/TryHackMe/intro-to-lan.png)

## Lessons Learned
- LAN topologies influence network layout, scalability, fault tolerance, and troubleshooting.
- Subnetting divides a larger IP network into smaller logical networks and helps organise address allocation.
- A subnet mask or CIDR prefix identifies the network portion of an IPv4 address.
- ARP resolves local IPv4 addresses to MAC addresses so Ethernet frames can reach the correct interface.
- ARP requests are generally broadcast on the local network, while ARP replies provide the requested mapping.
- ARP does not normally resolve the MAC address of a remote destination directly. A host typically resolves the MAC address of its default gateway instead.
- DHCP automates the assignment of IP addresses, subnet masks, default gateways, and DNS server settings.
- DHCP commonly uses a four-step exchange known as Discover, Offer, Request, and Acknowledge (DORA).
- The ARP cache and neighbour table can help troubleshoot local connectivity and investigate suspicious address mappings.
- Understanding LANs, subnetting, ARP, and DHCP is essential for network troubleshooting, packet analysis, and identifying threats such as ARP spoofing and rogue DHCP servers.

## How this connects to my Week 1 lab
My three VMs share one virtual LAN with a gateway and addresses assigned by DHCP, which is what I mapped in my network diagram.
