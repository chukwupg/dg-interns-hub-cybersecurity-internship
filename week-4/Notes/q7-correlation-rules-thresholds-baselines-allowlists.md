# Q7: Correlation rules, thresholds, baselines, allowlists

| Concept | What it is | When to use |
|---|---|---|
| Correlation rule | Combines multiple events/conditions into one alert (e.g. failed logon + successful logon from the same source right after) | When a single event alone isn't suspicious, but a sequence or combination is |
| Threshold | A simple count/rate limit that triggers an alert (e.g. 5 failures in 5 minutes) | Simple, well-understood attack patterns like brute force |
| Baseline | A profile of "normal" behavior (typical login times, typical process trees) used to spot deviations | Environments where "normal" varies a lot, so a fixed threshold would cause too many FPs or FNs |
| Allowlist | A list of known-good entities (IPs, hosts, users) excluded from a rule | Known scanners, admin jump boxes, scheduled jobs that would otherwise trigger an alert |

## How this shows up in my lab
- My brute-force detection (search #4) is a **threshold** rule: a fixed count (≥5) in a time window, not a baseline — I have no "normal" traffic profile built up in a one-day lab.
- A **correlation rule** I didn't build but could: failed Hydra attempts followed by a successful login from the same IP — that combination is far more suspicious than failures alone.
- An **allowlist** I'd want in a real deployment: my own Kali IP (192.168.98.130), since I generate attack traffic from it regularly in this lab and it would otherwise pollute every brute-force alert.