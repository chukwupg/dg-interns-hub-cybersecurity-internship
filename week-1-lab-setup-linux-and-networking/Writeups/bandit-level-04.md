# OverTheWire Bandit: Level 4 - Level 5

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 4 - 5 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is in the only human-readable file in the `inhere` directory. The other files are binary data and their names start with a dash.

## Connection
```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 3. (Not published here, per the internship rules.)

## Steps
1. Move into the `inhere` directory.

```bash
cd inhere
```

2. Check what type of data each file contains. The `./` prefix handles the leading dash in the names.

```bash
file ./*
```

3. Read the file reported as ASCII text. Filename: -file07

```bash
cat ./-file07
```

   Output:

```text
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
<level-password-redacted>
bandit4@bandit:~/inhere$
```

## Result
Password for Level 5 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 4 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-04.png)

## What I learned
- `file` identifies file types by content rather than by extension.
- Wildcards (`*`) let one command work on many files.
- Checking file type first avoids dumping binary data into the terminal.
- While checking each file one after the other will still work, it would be time consuming and would also mess-up the terminal. 