# Wireshark Filters: Meaning and When to Use It

| # | Filter | Meaning | When to use it |
|---|---|---|---|
| 1 | `ip.addr == 192.168.98.129` | Packets to or from this IP | Focus on one host |
| 2 | `ip.src == 192.168.98.129 && ip.dst == 192.168.98.129` | Traffic in one direction between two hosts | Follow a specific exchange |
| 3 | `tcp.port == 80` | TCP traffic on port 80 (either side) | Look at web traffic |
| 4 | `tcp.flags.syn==1 && tcp.flags.ack==0` | New connection attempts (SYN only) | Spot SYN scans and connection floods |
| 5 | `tcp.flags.syn==1 && tcp.flags.ack==1` | SYN/ACK replies | See which ports answered as open |
| 6 | `tcp.flags.reset==1` | RST packets | See closed ports and rejected connections |
| 7 | `tcp.flags.fin==1` | FIN packets | Look at teardown or FIN scans |
| 8 | `tcp.stream eq 0` | One whole TCP conversation | Follow a single connection |
| 9 | `tcp.analysis.retransmission` | Retransmitted packets | Find packet loss or blocked traffic |
| 10 | `http.request` | All HTTP requests | List what was requested |
| 11 | `http.request.method == "GET"` | HTTP GET requests | Check page or file requests |
| 12 | `http.response.code == 404` | HTTP "not found" responses | Spot guessing or scanning of paths |
| 13 | `dns` | All DNS traffic | General DNS review |
| 14 | `dns.flags.response == 0` | DNS queries only | See what hosts are asking for |
| 15 | `dns.qry.name contains "lab"` | DNS queries containing a name | Check lookups for a domain |
| 16 | `icmp` | All ICMP | Find pings and errors |
| 17 | `icmp.type == 8` | ICMP echo requests | Detect ping sweeps |
| 18 | `arp` | All ARP traffic | Look for ARP sweeps or spoofing |
| 19 | `smb` | SMB traffic | Review file-sharing activity |
| 20 | `tls.handshake.type == 1` | TLS Client Hello | See which servers a host starts TLS with |
