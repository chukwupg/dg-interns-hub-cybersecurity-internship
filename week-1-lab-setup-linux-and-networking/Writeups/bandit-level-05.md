# OverTheWire Bandit: Level 5 - Level 6

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 5 - 6 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is in a file somewhere under the `inhere` directory that is human-readable, 1033 bytes in size and not executable.

## Connection
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 4. (Not published here, per the internship rules.)

## Steps
1. Move into the `inhere` directory.

```bash
cd inhere
```

2. Search for regular files of exactly 1033 bytes that are not executable (`c` means bytes).

```bash
find . -type f -size 1033c ! -executable
```

3. Read the file that `find` returned. Path: `./maybehere07/.file2`

```bash
cat ./maybehere07/.file2
```

   Output:

```text
bandit5@bandit :~ /inhere$ cat ./maybehere07/.file2
<level-password-redacted>
```

## Result
Password for Level 6 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 5 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-05.png)

## What I learned
- `find` can filter by type (`-type f`), size (`-size 1033c`) and permissions (`! -executable`).
- Searching by file properties is much faster than opening files one by one.
- Initially I tried searching without specifying the permission, and the result still showed lots of files and some errors, but when I applied the permission, it narrowed down my search