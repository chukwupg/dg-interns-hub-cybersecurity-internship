# Q3. Capture filters vs display filters in Wireshark

## The difference
| | Capture filter | Display filter |
|---|---|---|
| When applied | Before capture; packets not matching are never saved | After capture; hides packets but keeps them in the file |
| Syntax | BPF (Berkeley Packet Filter) | Wireshark's own syntax |
| Can be changed mid-capture | No | Yes |
| Use when | Large captures, limited disk, you know what you want | Analysis, exploring, changing your mind |

## 10 working examples
| # | Type | Filter | What it shows |
|---|---|---|---|
| 1 | Capture | `host 192.168.98.129` | Only traffic to or from that host |
| 2 | Capture | `port 80` | Only port 80 traffic |
| 3 | Capture | `net 192.168.98.0/24` | Only traffic inside the lab subnet |
| 4 | Capture | `icmp` | Only ping and other ICMP |
| 5 | Capture | `udp port 53` | Only DNS over UDP |
| 6 | Display | `ip.addr == 192.168.98.129` | Packets to or from that IP |
| 7 | Display | `tcp.flags.syn==1 && tcp.flags.ack==0` | New connection attempts (SYN scan pattern) |
| 8 | Display | `http` | HTTP traffic |
| 9 | Display | `dns` | All DNS traffic |
| 10 | Display | `arp` | All ARP traffic |

## Tips
- A capture filter that is too strict can throw away evidence you can't get back.
- A display filter bar turns green when valid and red when the syntax is wrong.

## How this shows up in my lab
- I used the display filter in example 7 on my Nmap `-sS` captures for both the Ubuntu and Windows VMs.

- I saved a full capture and a filtered one (`full-traffic-capture.pcapng`, `filtered-traffic.pcapng`). 