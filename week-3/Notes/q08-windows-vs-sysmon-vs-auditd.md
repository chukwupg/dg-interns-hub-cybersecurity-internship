# Q8: Windows Event Log vs Sysmon vs Linux auditd

| Area | Windows Event Log | Sysmon | Linux auditd |
|---|---|---|---|
| What it captures | Logons, account changes, services, policy events | Process, network, file, registry, DNS activity | System calls, command execution, file access, logins |
| Log format | EVTX (structured XML) | EVTX (structured XML) | Text, `key=value` records in `/var/log/audit/audit.log` |
| Setup | Built in, tuned by audit policy | Install plus XML config | Install `auditd`, tuned by rules |
| Strength | Authentication and account activity | Deep process and network context | Kernel-level command and file auditing |
| Weakness | Little process detail by default | Only logs what config allows | Verbose, rules need tuning |
| SOC use | Detect brute force (4625), new users (4720) | Detect execution chains, C2, dropped files | Detect command abuse, sensitive file access |

## SOC use cases
- Windows Event Log: investigate logons and account creation.
- Sysmon: trace what a suspicious process did.
- auditd: see which user ran which command on a Linux server.
- Best used together, then sent to a SIEM.

## How this shows up in my lab
- Windows/Sysmon: the `net1 user` EID 1 event, the EID 3 connection and the `test.bat` EID 11 event.
    - See: [`Findings/sysmon-events](/week-3/Findings/sysmon-events/)
    
- Linux auditd: [[ausearch result for the nano install]]
- Compared: [[one sentence on what surprised you]]