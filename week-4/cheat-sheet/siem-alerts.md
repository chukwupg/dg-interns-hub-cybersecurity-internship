<!-- cheatsheet-siem-alerts.md -->
# Cheat Sheet: SIEM Alert — Likely Cause — First Check

| SIEM Alert | Likely Cause | First Check |
|---|---|---|
| Multiple failed SSH logins | Brute-force attempt, or a user/script with a stale saved password | `auth.log` for source IP and target user; count and timing of attempts |
| Multiple failed Windows logons (4625) | Brute-force attempt, locked-out account, misconfigured service account | Source IP/host, target account, failure reason code in the 4625 event |
| New user account created (4720) | Legitimate admin task, or attacker establishing persistence | Who created it (`Caller_User_Name`), whether it was scheduled/approved |
| PowerShell process spawned by unusual parent | Living-off-the-land technique, or a legitimate admin script | `ParentImage`/`CommandLine` fields, whether the parent process is expected (e.g. explorer.exe vs winword.exe) |
| Rare parent-child process pair | Malware execution chain, or a one-off legitimate admin tool | Compare against known-good baseline pairs; check the binary's path and signature |
| File integrity monitoring alert | Unexpected file change — could be an attacker or a legitimate update/patch | What changed, who/what process touched it, whether a deployment was scheduled |
| Sudden spike in log volume from one host | Misconfigured app, or a host under attack/compromise generating noise | Which sourcetype is spiking, correlate with other alerts on the same host |
| Alert firing from a known internal IP (e.g. your own Kali) | Your own authorized testing/scanning traffic | Confirm against your own test log/notes before escalating |
| Successful login immediately after failed attempts | Brute force that succeeded | Source IP, account, and whether this matches an authorized test or real external IP |
| Alert with no events shown in the underlying search | Index/sourcetype mismatch, forwarder stopped sending, or time range issue | Re-run the saved search manually with "All time"; check `index=_internal` for forwarder connectivity |