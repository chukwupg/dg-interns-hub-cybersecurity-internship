# Q6: Signature-based vs anomaly-based detection

## Definitions
- **Signature-based:** matches activity against known patterns (rules, hashes, strings, commands).
- **Anomaly-based:** builds a baseline of normal behaviour and flags what deviates from it.

## Comparison
| Area | Signature-based | Anomaly-based |
|---|---|---|
| How it detects | Matches known bad patterns | Flags deviation from a baseline |
| Strength | Accurate for known threats, easy to explain | Can spot new or unknown threats |
| Weakness | Misses new or modified attacks | More false positives, needs time to learn normal |
| Setup | Write or import rules | Needs baseline data and tuning |
| Alert clarity | Clear ("rule X matched") | Often needs analyst interpretation |

## Examples from a SOC perspective
| Type | Example |
|---|---|
| Signature | A Snort rule that alerts on an ICMP ping or an Nmap SYN scan pattern |
| Signature | Antivirus or EDR flagging a file whose hash matches known malware |
| Signature | A SIEM rule alerting on Event ID 4625 (failed logon) |
| Anomaly | A user who normally logs in 9am to 5pm suddenly logging in at 3am from a new location |
| Anomaly | A workstation sending far more outbound data than usual |
| Anomaly | A server that never ran PowerShell suddenly launching it |

## When to use which
- Signature-based for known, high-confidence threats and quick, clear alerts.
- Anomaly-based for insider threats, zero-days and subtle behaviour changes.
- A SOC normally combines both.

## How this shows up in my lab
- My four Snort rules are signature-based: each matches a fixed pattern (ICMP to my host, TCP to port 22, TCP to port 80, SYN packets).
- The T1046 rule adds a rate check (`detection_filter` with 20 SYN packets per second from one source). That is a rule with a threshold, not a learned baseline, so it sits between the two.
- Sysmon and auditd collect the data. Detecting that `net1.exe` created a user is signature-style (known command). Deciding it is unusual for that user or time would be anomaly-style.
- Evidence: Snort alerts in [Findings/snort-lab-notes.md`](/week-3/Findings/snort-lab-notes.md)