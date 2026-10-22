# OverTheWire Bandit: Level 7 - Level 8

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 7 - 8 |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Goal
The password is stored in `data.txt` next to the word `millionth`.

## Connection
```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 6. (Not published here, per the internship rules.)

## Steps
1. Confirm the file and its size.

```bash
ls 
```

2. Search the file for the keyword `millionth`.

```bash
cat data.txt | grep millionth 
```

   Output:

```text
bandit7@bandit :~ $ ls
data.txt
bandit7@bandit :~ $ cat data.txt | grep millionth
millionth    <level-password-redacted>
bandit7@bandit :~ $
```

## Result
Password for Level 8 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 7 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-07.png)

## What I learned
- `grep` searches text for a pattern and prints the matching lines.
- This is the same idea analysts use to search large log files.
