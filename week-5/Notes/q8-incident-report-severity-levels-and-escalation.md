# Q8. Incident Report, Severity Levels and Escalation

## Goal
Explain what goes into an incident report, how severity is set, and when to escalate.

## What goes into an incident report

| Section | What to include |
|---|---|
| Summary | What happened, when, what was affected, current status, in 3-5 sentences for non-technical readers |
| Timeline | Time-ordered events with timestamps and time zone: first activity, detection, response, resolution |
| IOCs | Hashes, IPs, domains, URLs (defanged), filenames, accounts, registry keys |
| Scope and impact | Affected systems, accounts and data; business impact; confirmed vs suspected |
| ATT&CK mapping | Techniques observed and the evidence for each |
| Root cause / initial access | How the attacker got in |
| Containment and eradication | Actions taken, by whom, when, and the result |
| Recovery | How systems were restored and verified |
| Recommendations | Prevention, detection improvements, process fixes, with owners |
| Lessons learned | What worked, what did not |

## Severity levels (example scale; organisations define their own)

| Level | Description | Example | Response expectation |
|---|---|---|---|
| Low | Minor, contained, no sensitive data affected | Blocked phishing email with no clicks | Handle in normal queue |
| Medium | Limited impact or possible compromise of one user or system | User clicked a phishing link, no credentials confirmed entered | Same-day response, monitor |
| High | Confirmed compromise or significant risk to important systems or data | Credentials stolen, malware executed on a workstation | Immediate response, escalate |
| Critical | Widespread impact, sensitive data loss or business outage | Ransomware spreading, domain admin compromised | Emergency response, executive notified |

Severity is based on impact, scope, data sensitivity and whether the attack is ongoing.

## Escalation

| Tier | Role | Typical actions |
|---|---|---|
| Tier 1 | Alert triage | Validate alerts, collect basic evidence, close false positives, escalate real incidents |
| Tier 2 | Incident analyst | Deeper investigation, scoping, containment, IOC extraction |
| Tier 3 / IR lead | Senior responder, threat hunter | Complex incidents, forensics, detection engineering |
| Management / legal / communications | Decision makers | Business decisions, legal and regulatory duties, customer and public messaging |

Escalate when severity is high or critical, sensitive data is involved, the attack is ongoing, the analyst lacks authority or skill to act, or legal and regulatory notification may be needed.

## Report template

```
INCIDENT REPORT
Incident ID: [[ ]]            Date/time detected: [[ ]] (time zone)
Analyst: [[ ]]                Report date: [[ ]]
Status: [[open / contained / closed]]
Severity: [[Low/Medium/High/Critical]] - Justification: [[ ]]

1. SUMMARY
[[3-5 sentences: what, when, where, impact, status]]

2. TIMELINE
| Time (UTC/local) | Event | Source/evidence |
| [[ ]] | [[ ]] | [[ ]] |

3. SCOPE AND IMPACT
Affected systems/accounts/data: [[ ]]
Confirmed vs suspected: [[ ]]

4. IOCs (defanged)
| Type | Value | Source | Reputation |
| [[ ]] | [[ ]] | [[ ]] | [[ ]] |

5. ATT&CK MAPPING
| Technique ID | Name | Evidence |
| [[ ]] | [[ ]] | [[ ]] |

6. ROOT CAUSE / INITIAL ACCESS
[[ ]]

7. CONTAINMENT, ERADICATION, RECOVERY
| Action | Time | Owner | Result |
| [[ ]] | [[ ]] | [[ ]] | [[ ]] |

8. RECOMMENDATIONS
Prevention: [[ ]]
Detection improvements: [[ ]]
Process: [[ ]]

9. LESSONS LEARNED
[[ ]]

Attachments: [[screenshots, logs, hashes]]
```

## How this shows up in my lab
- My Week 5 incident report covers one case: [[phishing sample / Malware-Traffic-Analysis exercise / Atomic test]]
- I use this template, with evidence from Sysmon and Splunk (`lab` index): [[search used and result count]]
- Severity I assigned and why: [[ ]]
- Detection improvements I recommend (for example, testing the "New User Created" alert properly): [[ ]]