# Q6. 15 key Windows Security Event IDs

| Event ID | Meaning | When to use it |
|---|---|---|
| 4624 | An account successfully logged on (includes logon type) | Check who logged on, how and from where |
| 4625 | An account failed to log on | Brute force and password-guessing detection |
| 4634 | An account was logged off | Work out session length; pair with 4624 |
| 4648 | A logon was attempted with explicit credentials | Spot `runas`, `net use /user`, possible lateral movement |
| 4672 | Special privileges assigned to a new logon | Find admin-level logons |
| 4688 | A new process was created | Hunt for suspicious programs (command line needs extra policy) |
| 4697 | A service was installed on the system | Detect new services used for persistence |
| 4720 | A user account was created | Detect rogue new accounts |
| 4722 | A user account was enabled | Check a disabled account being switched back on |
| 4724 | An attempt was made to reset an account's password | Detect password resets by someone else |
| 4732 | A member was added to a security-enabled local group | Detect additions to Administrators |
| 4768 | A Kerberos ticket-granting ticket was requested | Domain logon activity on a domain controller |
| 4769 | A Kerberos service ticket was requested | Domain access to services; used in Kerberos attack hunting |
| 4776 | The domain controller (or local system) attempted to validate credentials (NTLM) | NTLM logon attempts and failures |
| 1102 | The audit log was cleared | A strong sign someone is covering tracks |

## Not in the Security log
- **7045** (System log, Service Control Manager) records a new service being installed. It is a good partner to 4697.

## How this shows up in my lab
- I generated and found 4625, 4624, 4720, 4732, 7045 and 1102 on my Windows VM. 
Check [windows-events](/Findings/windows-events/)

- My 4720, then 4732, then 4624 (type 2) sequence for `labtest` is a pattern an analyst would flag.

- 4768, 4769 and 4776 mostly apply in a domain; my lab has no domain controller.