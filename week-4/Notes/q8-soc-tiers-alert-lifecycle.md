# Q8: SOC tiers and the alert lifecycle

## SOC tiers
| Tier | Role |
|---|---|
| L1 | First responder — triages incoming alerts, does initial investigation, escalates if needed |
| L2 | Deeper investigation — confirms/denies the L1 escalation, starts containment, may hunt further |
| L3 | Senior/expert — handles the most complex incidents, threat hunting, rule tuning, forensics |

## Alert lifecycle
`Alert generated → Triage (L1) → Investigate → Verdict (TP/FP) → Escalate (if TP) or close (if FP) → Remediate/contain → Document/close → Feed back into tuning`

## Five questions every triage note must answer
1. **Who** — which user/account/host is involved?
2. **What** — what activity triggered the alert?
3. **When** — timestamp(s) of the activity?
4. **Where** — source and destination (IP, host, port)?
5. **Why** — why did this trigger, and is it malicious or benign (verdict)?

## How this shows up in my lab
- My own setup is a one-person "SOC," so I played all three tiers at once: I generated the Hydra attack (as the attacker), then triaged it myself (as L1) by checking the raw event and parsed fields.
- My 3 triage notes (in the Findings folder) answer who/what/when/where/why for the alerts I picked, which is the same structure a real L1 analyst would use on shift.