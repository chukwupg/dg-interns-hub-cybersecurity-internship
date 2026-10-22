# OverTheWire Bandit: Level 10 - Level 11

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 10 - 11 |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Goal
The password is in `data.txt`, which contains Base64-encoded data.

## Connection
```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 9. (Not published here, per the internship rules.)

## Steps
1. Decode the Base64 content.

```bash
base64 -d data.txt
```

   Output:

```text
bandit10@bandit :~ $ base64 -d data.txt
The password is <redacted>
bandit10@bandit :~ $
```

## Result
Password for Level 11 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 10 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-10.png)

## What I learned
- Base64 is an encoding, not encryption. Anyone can reverse it without a key.
- Encoded data often appears in logs, emails and malware, so it is worth recognising.