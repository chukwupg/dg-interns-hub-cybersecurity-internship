# Basic Port Scans (TryHackMe)

**Link:** https://tryhackme.com/room/nmap02

## Goal
Understand TCP and UDP ports, TCP flags, and how connect, SYN and UDP scans decide a port's state. [[Rewrite]]

## Task-by-task
| Task | What it covered | My note |
|---|---|---|
| 1. Introduction | Room setup, prerequisites and learning objectives | Set up the AttackBox and target machine. Reviewed the Nmap scanning process and identified port scanning as the next stage after target enumeration, host discovery and reverse DNS lookup. |
| 2. TCP and UDP Ports | Port numbers, network services and port states | Learned how TCP and UDP ports identify services running on a host and the six Nmap port states: `open`, `closed`, `filtered`, `unfiltered`, `open|filtered` and `closed|filtered`. |\
| 3. TCP Flags | TCP header structure and control flags | Studied the six TCP control flags: URG, ACK, PSH, RST, SYN and FIN, and how they control connection establishment, acknowledgement, data transmission and termination. |
| 4. TCP Connect Scan | Full TCP three-way handshake | Learned how `-sT` establishes a complete TCP three-way handshake to identify open ports. Examined SYN, SYN/ACK, ACK and RST/ACK packet exchanges using Wireshark. Also explored `-F` for fast scanning and `-r` for sequential port scanning. |
| 5. TCP SYN Scan | Half-open TCP scanning | Learned how `-sS` identifies open TCP ports without completing the three-way handshake. Requires root privileges, is generally faster than TCP Connect scans and is Nmap's default when run with sufficient privileges. |
| 6. UDP Scan | Connectionless port scanning | Learned how `-sU` identifies UDP services using response behaviour. Closed ports typically return ICMP Type 3, Code 3 (Port Unreachable), while open ports may not respond. Used `--top-ports` to limit scan scope and improve performance. |
| 7. Fine-Tuning Scope and Performance | Port selection, scan timing and parallelisation | Learned to customise scan scope using `-p`, `-p-`, `-F` and `--top-ports`. Explored timing templates (`-T0` to `-T5`), packet rate controls (`--min-rate`, `--max-rate`) and probe parallelisation (`--min-parallelism`, `--max-parallelism`) to balance scan speed, accuracy and network impact. |

## Port states
| State | Meaning |
|---|---|
| open | A service is listening |
| closed | Reachable, nothing listening |
| filtered | Probe blocked, state unknown |
| open\|filtered | No reply, can't tell (common in UDP) |

## Commands used
| Command | What it does |
|---|---|
| `nmap -sT <target>` | TCP connect scan |
| `sudo nmap -sS <target>` | SYN scan |
| `sudo nmap -sU <target>` | UDP scan |
| `nmap -p <ports>`, `-p-`, `-F`, `--top-ports <n>` | Choose ports |
| `nmap -T<0-5>`, `--min-rate <n>` | Timing and speed |


## Screenshot
![nmap basic port scans room](/Findings/TryHackMe/nmap-basic-port-scans.png)

## What I Learned

- Port scanning helps identify open, closed and filtered ports, revealing which services are accessible on a target system.
- TCP and UDP use different communication mechanisms, so their scanning techniques and responses differ.
- TCP has six control flags: SYN, ACK, FIN, RST, PSH and URG. Understanding these flags helps explain how Nmap performs different scan types.
- TCP Connect scans (`-sT`) complete the three-way handshake, while SYN scans (`-sS`) use a half-open approach by sending a reset instead of completing the connection.
- UDP scans (`-sU`) are less straightforward because open ports may not respond, while closed ports typically return ICMP Port Unreachable messages.
- Nmap supports different scan types, including TCP Connect, SYN, UDP, NULL, FIN and Xmas scans. Each uses different packet characteristics to identify port states.
- Port states such as `open`, `closed`, `filtered`, `unfiltered`, `open|filtered` and `closed|filtered` describe what Nmap can determine from its probes and the responses received.
- Nmap's host discovery options help identify active systems before scanning their ports, while `-Pn` skips host discovery and treats targets as online.
- Port selection options such as `-p`, `-p-`, `-F` and `--top-ports` allow scans to be tailored to specific ports or scanning requirements.
- Timing and performance options, including `-T0` to `-T5`, `--min-rate`, `--max-rate` and parallelism controls, help manage scan speed and network traffic.
- The Nmap Scripting Engine (NSE) extends scanning capabilities through scripts for service discovery, vulnerability detection, authentication checks and other enumeration tasks.
- NSE scripts can be selected using `--script`, configured with `--script-args` and explored through `--script-help` or the official Nmap script documentation.
- Firewall evasion options such as `-f`, `--mtu`, `--scan-delay` and `--badsum` modify how probes are transmitted, although they do not guarantee that a scan will evade detection.
- Wireshark provides packet-level visibility into Nmap scans, making it useful for understanding TCP handshakes, flag combinations, scan behaviour and target responses.
- Practical scanning reinforces the importance of choosing appropriate scan types, port ranges and timing options based on the target environment and assessment objectives.

## How this shows up in my lab
- My -sS scan of 192.168.98.129 showed 3 ports, with Apache on port 80 after I installed it.

    ![ubuntu SYN scan](/Findings/nmap/ubuntu/nmap-tcp-syn-scan.png)

- In Wireshark the scan appeared as many SYN packets from Kali, with RST replies from closed ports.
