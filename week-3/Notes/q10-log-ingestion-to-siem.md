# Q10: Log ingestion and the flow from log source to SIEM dashboard

## What is log ingestion?
- Collecting logs from many sources, converting them into a common format, and storing them in one searchable place.
- Goal: one place to search, correlate events and alert.

## General flow
| Stage | What happens |
|---|---|
| 1. Log source | Endpoints, servers, firewalls, IDS, applications create logs |
| 2. Collection | An agent or forwarder reads the logs, or the source sends them (syslog, API) |
| 3. Transport | Logs travel to a central server, usually encrypted |
| 4. Parsing / normalisation | Raw text is split into fields (time, user, IP, event ID) |
| 5. Storage / indexing | Data is stored and indexed for fast searching |
| 6. Detection | Rules and correlation create alerts |
| 7. Dashboard / alert | Analysts view dashboards, investigate and respond |

## Wazuh
| Component | Role |
|---|---|
| Wazuh agent | Installed on endpoints, collects logs and events from configured sources |
| Wazuh server | Analyses data from agents using decoders and rules, including threat intelligence |
| Wazuh indexer | Stores and indexes alerts, searchable |
| Wazuh dashboard | Web interface for visualisation, threat hunting and management |
- Wazuh can also take agentless input, for example syslog from firewalls or network IDS.
- The agent does not know what to collect on its own, so you configure its log sources.

## Splunk (general architecture)
| Component | Role |
|---|---|
| Forwarder (for example Universal Forwarder) | Sends logs from endpoints |
| Indexer | Parses and stores data |
| Search head | Searches data and runs dashboards and alerts |

## Example flow
- Windows endpoint creates a Sysmon event, the agent forwards it, the server decodes it with a rule, the indexer stores it, and the dashboard shows an alert or a count of Event ID 1.

## How this shows up in my lab
- My log sources: Sysmon on Windows (Operational log), auditd on Ubuntu (`/var/log/audit/audit.log`) and Snort alerts.
- I did not install Wazuh or Splunk this week, so I looked at each source by hand: Event Viewer, `ausearch` and the Snort console.
- With a SIEM, an agent on the Windows VM could read the Sysmon log and one on Ubuntu could read the audit log. Both would reach one server, and the dashboard could show counts of Sysmon Event ID 1 and 3.
- Time zones differ across sources: Sysmon `UtcTime` is UTC, auditd and Snort use local time (WAT), which a SIEM must normalise.