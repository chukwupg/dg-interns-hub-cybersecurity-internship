# OverTheWire Bandit: Level 9 - Level 10

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 9 - 10 |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Goal
The password is in `data.txt`, which is mostly binary. It is one of the few human-readable strings, preceded by several `=` characters.

## Connection
```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 8. (Not published here, per the internship rules.)

## Steps
1. Extract printable strings from the binary file and filter for the `=` marker.

```bash
strings data.txt | grep "=="
```

   Output:

```text
bandit9@bandit:~$ strings data.txt | grep '=='
^========== the
========== password
========== is
========== <redacted>
bandit9@bandit:~$
```

## Result
Password for Level 10 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 9 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-09.png)

## What I learned
- Cat when piped to grep feeds the file through standard input, so if the file contains any binary character, grep prints a warning instead of the matching lines. 
- `strings` pulls readable text out of binary files. It is common in malware analysis and forensics.
- Piping `strings` into `grep` narrows the results quickly.
