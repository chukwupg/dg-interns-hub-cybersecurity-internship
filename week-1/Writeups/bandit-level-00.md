# OverTheWire Bandit: Level 0 - Level 1

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 0 - 1 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
Log in to the Bandit server over SSH (port 2220) as `bandit0` and read the password for the next level from a file named `readme` in the home directory.

## Connection
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
The password for `bandit0` is given on the Level 0 page of the Bandit website.

## Steps
1. List the files in the home directory.

```bash
ls
```

2. Read the `readme` file.

```bash
cat readme
```

   Output:

```text
Windows PowerShell

bandit0@bandit :~ $ ls
readme
bandit0@bandit :~ $ cat readme
Congratulations on your first steps into the bandit game !!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: <redacted>

bandit0@bandit :~ $
```

## Result
Password for Level 1 found: `[REDACTED]` (not published, per the rules).

## Screenshot

![Bandit level 0 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-00.png)

## What I learned
- How to connect to a remote machine with SSH, including a non-default port (`-p 2220`).
- `ls` lists files and `cat` prints a file's content directly on the terminal.
