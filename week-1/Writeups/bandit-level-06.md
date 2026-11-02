# OverTheWire Bandit: Level 6 - Level 7

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 6 - 7 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is in a file somewhere on the server that is owned by user `bandit7`, owned by group `bandit6` and exactly 33 bytes in size.

## Connection
```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 5. (Not published here, per the internship rules.)

## Steps
1. Search the whole filesystem and send permission-denied errors to `/dev/null` to keep the output clean.

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

2. Read the file that `find` returned. Path: `/var/lib/dpkg/info/bandit7.password`

```bash
cat /var/lib/dpkg/info/bandit7.password
```

   Output:

```text
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
<level-password-redacted>
bandit6@bandit:~$
```

## Result
Password for Level 7 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 6 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-06.png)

## What I learned
- `find` can match file owner (`-user`) and group (`-group`).
- `2>/dev/null` discards error messages (standard error). It is useful when searching from `/`.
- File ownership is a core part of Linux permissions.
