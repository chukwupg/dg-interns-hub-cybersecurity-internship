# Event ID / Rule - What It Means - When to Use It

| Event ID / Rule | Source | What It Means | When to Use It |
|---|---|---|---|
| 4624 | Windows Security | Successful logon | Investigating normal vs. anomalous logins |
| 4625 | Windows Security | Failed logon | Detecting brute force attempts |
| 4672 | Windows Security | Special privileges assigned to a new logon | Spotting admin-level logons |
| 4688 | Windows Security | Process creation | Tracking program execution (command line needs audit policy enabled) |
| 4720 | Windows Security | New user account created | Detecting persistence (T1136) |
| 1 | Sysmon | Process Create (image, command line, parent, hashes) | Monitoring process execution |
| 3 | Sysmon | Network Connection (process, source/destination IP and port) | Detecting C2 or lateral movement |
| 11 | Sysmon | File Create (which process wrote which file) | Detecting dropped files |
| 13 | Sysmon | Registry Value Set | Detecting registry-based persistence |
| 22 | Sysmon | DNS Query (process and queried name) | Detecting DNS-based C2 |
| EXECVE | auditd | Command execution with every argument | Auditing Linux commands |
| USER_LOGIN | auditd | User login event | Tracking Linux authentication |
| USER_AUTH | auditd | Authentication attempt | Detecting failed logins |
| CONFIG_CHANGE | auditd | Audit configuration or rule changed | Detecting tampering with auditing |
| 1000001 | Snort | ICMP Ping Detected | Detecting network reconnaissance |
| 1000002 | Snort | SSH Connection Attempt | Monitoring SSH access |
| 1000003 | Snort | HTTP Traffic | Monitoring web traffic |
| 1000004 | Snort | Nmap SYN Scan Detected (MITRE T1046) | Detecting port scanning |

## Seen in my lab
| Item | Where I saw it |
|---|---|
| Sysmon 1 | `powershell.exe` launch, and `net1.exe` creating a user |
| Sysmon 3 | PowerShell connection 192.168.98.131 to 192.168.98.129:8000 |
| Sysmon 11 | `test.bat` on the Desktop (a `.txt` file did not log under the config) |
| auditd EXECVE / CONFIG_CHANGE | `sudo auditctl ...` command and rule add, on Ubuntu |
| Snort 1000001 to 1000004 | All four fired from Kali (ping, curl, SSH test, Nmap SYN scan) |
