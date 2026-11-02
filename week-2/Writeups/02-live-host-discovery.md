# Live Host Discovery (TryHackMe)

**Link:** https://tryhackme.com/room/nmap01

## Goal
Learn how to find which hosts are up on a network before port scanning, using different layers of the TCP/IP model. [[Rewrite]]

## Task-by-task

## Task-by-task


## Nmap Live Host Discovery – Task Notes

| Task | What it covered | My note |
| ---- | --------------- |-------- |
| 1. Introduction                                       | Why discover live hosts before port scanning                | Host discovery identifies active systems before port scanning, saving time and reducing unnecessary network traffic. Nmap can use ARP, ICMP, TCP and UDP probes to identify reachable hosts.                                            |
| 2. Subnetworks                                        | Subnets, network segments and CIDR ranges                   | A network segment is a physical connection, while a subnet is a logical IP network. ARP operates within the local subnet and cannot cross routers; `/16` and `/24` define different network sizes.                                      |
| 3. Understanding Host Discovery through TCP/IP Layers | Discovery using Link, Network and Transport layer protocols | Nmap uses ARP at the Link Layer, ICMP at the Network Layer, and TCP/UDP at the Transport Layer. Different probes help identify live hosts when particular protocols are blocked.                                                        |
| 4. Enumerating Targets                                | Specifying target IPs, ranges, subnets and input files      | Nmap accepts individual IPs, hostnames, ranges, CIDR notation and target lists using `-iL`. The `-sL` option lists scan targets without probing them, while `-n` disables DNS resolution.                                               |
| 5. Nmap Host Discovery Using ARP                      | Discovering live hosts on the local subnet                  | ARP discovery uses broadcast requests to obtain target MAC addresses. Use `nmap -PR -sn TARGETS` to perform ARP-only host discovery without port scanning.                                                                              |
| 6. Nmap Host Discovery Using ICMP                     | Echo, timestamp and address mask probes                     | Nmap supports ICMP Echo (`-PE`), Timestamp (`-PP`) and Address Mask (`-PM`) discovery. Since firewalls may block specific ICMP types, using alternative probes improves host discovery coverage.                                        |
| 7. Nmap Host Discovery Using TCP and UDP              | TCP SYN, TCP ACK and UDP ping techniques                    | TCP SYN (`-PS`) and ACK (`-PA`) probes identify hosts through TCP responses, while UDP (`-PU`) can trigger ICMP Port Unreachable responses from closed ports. The appropriate probe depends on network filtering and access privileges. |
| 8. Using Reverse-DNS Lookup                           | Resolving IP addresses to hostnames                         | Reverse DNS maps IP addresses to hostnames, helping identify systems and their possible roles. Use `-R` to force reverse lookups for all targets, `-n` to disable DNS resolution, and `--dns-servers` to specify a DNS server.          |

## Commands used
| Command | What it does |
|---|---|
| `nmap -sL <range>` | List targets without scanning |
| `nmap -sn <range>` | Host discovery only, no port scan |
| `nmap -PR -sn <range>` | ARP discovery |
| `nmap -PE / -PP / -PM -sn <range>` | ICMP echo / timestamp / address mask |
| `nmap -PS / -PA / -PU -sn <range>` | TCP SYN / TCP ACK / UDP ping |
| `nmap -n` / `nmap -R` | Skip / force reverse DNS |

## Screenshot
![nmap live host discovery room](/Findings/TryHackMe/live-host-discovery.png)

## What I Learned

- Host discovery is an important reconnaissance step because it identifies active systems before port scanning.
- Network segments represent physical connectivity, while subnets represent logical IP network divisions.
- ARP operates at Layer 2 and can discover hosts on the local subnet, but it cannot cross routers.
- Nmap supports multiple host discovery techniques across the TCP/IP stack: ARP, ICMP, TCP and UDP.
- The `-sn` option performs host discovery without proceeding to port scanning.
- Target specification supports individual IPs, hostnames, IP ranges, CIDR notation and input files using `-iL`.
- ICMP discovery includes Echo (`-PE`), Timestamp (`-PP`) and Address Mask (`-PM`) requests. A lack of response does not necessarily mean a host is offline.
- TCP SYN (`-PS`) and TCP ACK (`-PA`) pings use TCP responses to determine whether a target is reachable. Privileged and unprivileged users may generate these probes differently.
- UDP ping (`-PU`) can identify a live host when a closed UDP port responds with an ICMP Port Unreachable message.
- Different discovery probes can produce different results depending on firewall rules and network filtering. Combining techniques can improve discovery coverage.
- Reverse DNS (`-R`) can reveal hostnames and provide additional information about network infrastructure, while `-n` disables DNS resolution.
- Wireshark helps validate Nmap's discovery techniques by showing the actual packets exchanged during scans.

## How this shows up in my lab
- I performed `nmap -sn` scan twice from kali on 192.168.98.0/24 network, one when the Ubuntu machine was up and the second was when the Windows machine was up, for each case, I found 2 hosts: Kali IP and my lab machine IPs.
    **Ubuntu**
    ![Ubuntu host discovery](/Findings/nmap/ubuntu/nmap-host-discovery.png)
    **Windows**
    ![Windows host discovery](/Findings/nmap/windows/host-discovery.png)

- Because my VMs share one subnet, discovery used ARP or ICMP

- Reverse DNS ties to my dnsmasq setup on Ubuntu (192.168.98.129), where I resolved `ubuntu.lab`. 

    ![dns resolution](/Findings/wireshark/dns-query.png)