# Q1: What is a SIEM? Components, data flow, and SIEM vs log management vs SOAR vs EDR

## What is a SIEM?
A SIEM (Security Information and Event Management) collects logs and events from many sources, normalizes them into a common format, correlates them against rules, and surfaces alerts for analysts to investigate.

## Components
- **Collection**: agents/forwarders, syslog, APIs pull or receive raw logs.
- **Parsing/normalization**: raw log text is mapped into structured fields (source IP, user, event type).
- **Indexing/storage**: normalized events are stored for fast search.
- **Correlation engine**: rules/searches compare events against known bad patterns or thresholds.
- **Alerting**: matches trigger notifications.
- **Dashboards/search**: analysts query and visualize data.

## Data flow
`Log source → Forwarder/Agent → Parsing/normalization → Indexer (storage) → Correlation/search → Alert → Analyst (dashboard/search head)`

## Comparison table

| Tool | Primary job | Stores raw logs? | Correlates across sources? | Automates response? | Example |
|---|---|---|---|---|---|
| SIEM | Centralize + correlate security events, alert | Yes | Yes | Limited (alerting only) | Splunk, Wazuh |
| Log management | Centralize + search logs | Yes | Minimal | No | Graylog, ELK (plain) |
| SOAR | Automate response to alerts (playbooks) | No (consumes SIEM data) | No (acts on SIEM output) | Yes | Shuffle, Tines |
| EDR | Monitor + respond on individual endpoints | Partial (endpoint-local) | No (endpoint-scoped) | Yes (isolate host, kill process) | CrowdStrike, Wazuh agent (partially) |

## How this shows up in my lab
- My Splunk instance is acting as both the log management layer (storing Windows, Sysmon, and `auth.log` events in the `lab` index) and the SIEM layer (the 5 SPL searches and 2 scheduled alerts I built are the correlation/alerting part).
- I have no SOAR or EDR in this lab, alerts just notify, they don't trigger automated action. That's a limitation I can call out in the report.