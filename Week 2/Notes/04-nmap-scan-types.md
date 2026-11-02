# Q4. Nmap scan types: how they work and what they leave behind

| Option | How it works | What it leaves in packets | What it leaves in logs |
|---|---|---|---|
| `-sn` | Host discovery only, no port scan. On the local subnet it uses ARP; elsewhere ICMP echo and a few TCP probes | ARP requests across the range, or ICMP echo requests | Little on hosts; firewall or IDS may log the sweep |
| `-sS` | SYN ("half-open") scan. Sends SYN, then RST after a SYN/ACK; needs root | Many SYNs; SYN/ACK from open ports, RST from closed ones, never a full handshake | Applications often don't log it; firewalls and IDS do |
| `-sT` | Connect scan. Completes the full handshake; no root needed | Full SYN, SYN/ACK, ACK then RST or FIN | Services may log short connections |
| `-sU` | UDP scan. Sends UDP probes; slow | UDP packets; ICMP "port unreachable" from closed ports; no reply may mean open\|filtered | Few service logs; firewall logs |
| `-sV` | Service/version detection. Connects to open ports and sends probes to read banners | Extra application-level requests after the handshake | Service logs may show odd requests |
| `-O` | OS fingerprinting. Sends crafted TCP, UDP and ICMP probes and compares replies | Unusual packets to open and closed ports | Mostly firewall/IDS |
| `-A` | Aggressive: version detection, OS detection, default scripts, traceroute | All of the above, and the loudest | Most noticeable in logs |

## Defender view
- `-sS` is quieter in application logs but leaves a clear SYN pattern in a packet capture.
- The more options used, the more noise.

## Only scan what you own
- I scanned only my own VMs in an isolated lab. Scanning other systems without permission is not allowed.

## How this shows up in my lab
- I ran `-sn`, `-sS`, `-sV`, `-O` and `-A` against my Ubuntu VM and my Windows VM and saved output with `-oN` and `-oX`.

- The `-sS` captures (`ubuntu-nmap-scan-traffic.pcapng`, `windows-nmap-scan-traffic.pcapng`) show the SYN burst.
