# Q5: TP, FP, TN, FN, alert fatigue, and tuning

| Term | Meaning | Example |
|---|---|---|
| True positive (TP) | Alert fired, and it really was malicious/bad activity | My Hydra attack triggered the "SSH Bruteforce" alert — correct |
| False positive (FP) | Alert fired, but the activity was actually benign | A sysadmin typing their password wrong 5 times triggers the same alert, but it's not an attack |
| True negative (TN) | No alert, and nothing bad happened | Normal login during business hours, no alert — correct |
| False negative (FN) | No alert, but something bad actually happened | A slow brute force (1 attempt every 10 minutes) stays under my `count >= 5` threshold and never fires |
| Alert fatigue | Analysts become desensitized to alerts because too many are low-value/false positives, and start ignoring or rushing through them | A rule that fires on every failed login, even a single typo, floods the queue |
| Tuning | Adjusting thresholds, allowlists, or rule logic to reduce FPs/FNs while keeping real detections | Raising my brute-force threshold from `count >= 3` to `count >= 5`, or allowlisting a known vulnerability scanner's IP |

## How this shows up in my lab
- My SSH Bruteforce alert (`count >= 5` in 5-15 min) is a TP when it caught my Hydra run (~20 attempts from one IP in seconds).
- If I ran this in a shared lab where my own typos triggered it, that would be a FP — a case for tuning the threshold up or adding my own IP to an allowlist.
- Without a slow-brute-force detection (e.g. over hours), a patient attacker could stay under my threshold — a FN I should mention as a limitation.