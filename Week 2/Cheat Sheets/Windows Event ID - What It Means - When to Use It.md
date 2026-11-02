# Windows Event ID – What It Means – When to Use It

| # | Event ID | What it means | When to use it |
|---|---|---|---|
| 1 | 4624 | Successful logon (check logon type) | See who got in and how |
| 2 | 4625 | Failed logon | Detect brute force or password guessing |
| 3 | 4634 | Logoff | Measure session length |
| 4 | 4648 | Logon with explicit credentials | Spot `runas` or lateral movement |
| 5 | 4672 | Special privileges assigned | Find admin-level logons |
| 6 | 4688 | New process created | Hunt for suspicious programs |
| 7 | 4697 | Service installed (Security log) | Catch service-based persistence |
| 8 | 4720 | User account created | Detect rogue accounts |
| 9 | 4722 | User account enabled | Check re-enabled accounts |
| 10 | 4724 | Password reset attempt | Detect resets by another user |
| 11 | 4732 | Member added to local group | Detect additions to Administrators |
| 12 | 4768 | Kerberos TGT requested | Domain logon activity |
| 13 | 4769 | Kerberos service ticket requested | Domain service access, Kerberos hunting |
| 14 | 4776 | Credential validation (NTLM) | Track NTLM attempts and failures |
| 15 | 1102 | Audit log cleared | Detect log tampering |

**Extra:** 7045 (System log) is a new service installed. Use it with 4697.
