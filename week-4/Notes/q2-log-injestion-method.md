# Q2: Log ingestion methods and Splunk Universal Forwarder vs Wazuh agent

## Ingestion methods
| Method | How it works | Example use |
|---|---|---|
| Agent | Small program installed on the host, reads local logs/events, ships them out | Splunk UF, Wazuh agent |
| Syslog | Host sends logs over the syslog protocol (UDP/TCP 514) to a central receiver | Network devices, firewalls |
| API | Pull logs from a service's API on a schedule | Cloud platforms (AWS CloudTrail, M365) |
| File monitoring | Watch a log file/directory for new lines and forward them | Watching `/var/log/auth.log` |

## Splunk Universal Forwarder vs Wazuh agent

| | Splunk Universal Forwarder | Wazuh agent |
|---|---|---|
| What it sends | Raw/structured logs (files, Windows Event Log, etc.) | Logs + security telemetry (FIM, rootkit checks, vulnerability data) |
| Where it sends | Splunk indexer (port 9997) | Wazuh manager (port 1514) |
| Parsing | Minimal on the forwarder; heavy parsing happens at the indexer/search head | Agent does light parsing; manager applies decoders/rules |
| Extra features | Lightweight, forwarding-only | Built-in FIM, log analysis, active response, vulnerability detection |
| Footprint | Very light | Light, but does more work locally |

## How this shows up in my lab
- I used the Splunk Universal Forwarder on my Windows VM ([[WINDOWS_HOSTNAME]]) to send Security and Sysmon logs, and on my Ubuntu VM (192.168.98.129) to monitor `/var/log/auth.log`. Both just forward — all the real parsing and correlation happened in Splunk itself.
- I did not get to install the Wazuh agent this week due to RAM limits (Splunk already uses most of my 8 GB host), so I'm documenting the Wazuh agent from research rather than from my own install.