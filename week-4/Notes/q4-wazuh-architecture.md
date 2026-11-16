# Q4: Wazuh architecture, decoders/rules, and rule levels 0-15

## Architecture
- **Agent**: installed on the monitored host, collects logs, FIM data, and security telemetry, sends to the manager.
- **Manager**: receives agent data, runs it through decoders and rules, generates alerts, stores them.
- **Indexer** (Wazuh indexer, OpenSearch-based): stores the processed alerts/events for search.
- **Dashboard**: web UI (OpenSearch Dashboards-based) for browsing alerts, agent status, and FIM results.

Data flow: `Agent → Manager (decode + rule match) → Indexer (storage) → Dashboard (search/visualize)`

## Decoders and rules
- **Decoders** parse raw log text into structured fields (e.g. pull `srcip`, `user` out of an SSH log line). They run first.
- **Rules** match on the decoded fields (and can reference other rules via `if_matched_sid`) to decide if something is worth alerting on, and assign a severity level.
- A rule can build on a lower-level base rule (e.g. "SSH auth failed" rule 5716) and add correlation logic (e.g. "5+ times from the same IP") to create a higher-severity custom rule.

## Rule levels 0-15
| Level range | Meaning |
|---|---|
| 0 | Informational, not shown as an alert by default |
| 1-5 | Low severity: minor issues, noise, routine events |
| 6-9 | Medium severity: suspicious but not confirmed malicious |
| 10-12 | High severity: likely attack or policy violation (e.g. correlated brute force) |
| 13-15 | Critical: confirmed compromise indicators, highest priority |

## How this shows up in my lab
- I did not install Wazuh this week due to RAM limits (Splunk already uses most of my host's 8 GB), so this is from documentation, not my own install.
- I wrote a custom rule (ID 100010, level 10) that builds on base rule 5716 and uses `<same_source_ip/>` to flag repeated SSH failures from one IP — mirroring the exact Hydra brute force I ran and captured in Splunk, but I was not able to run `wazuh-logtest` against it.