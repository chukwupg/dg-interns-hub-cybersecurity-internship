# OverTheWire Bandit: Level 8 - Level 9

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 8 - 9 |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Goal
The password is the only line in `data.txt` that appears exactly once.

## Connection
```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 7. (Not published here, per the internship rules.)

## Steps
1. `uniq -u` prints lines that occur once, but it only compares adjacent lines, so sort the file first.

```bash
sort data.txt | uniq -u
```

   Output:

```text
bandit8@bandit:~$ sort data.txt | uniq -u
<level-password-redacted>
bandit8@bandit:~$
```

## Result
Password for Level 9 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 8 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-08.png)

## What I learned
- Sort command arranges lines of text and outputs the sorted result.
- `uniq` only detects duplicates that are next to each other, so `sort` must come first.
- The pipe (`|`) sends one command's output into the next command.
- Combining small tools is a core Linux skill and can reduce the time it takes to achieve a designated task.
