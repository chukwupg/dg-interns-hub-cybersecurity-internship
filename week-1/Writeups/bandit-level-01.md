# OverTheWire Bandit: Level 1 - Level 2

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 1 - 2 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is stored in a file called `-` in the home directory.

## Connection
```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 0. (Not published here, per the internship rules.)

## Steps
1. List the home directory and confirm the file exists.

```bash
ls
```

   Output:

```text
[[paste your terminal output here; replace any password with [REDACTED]]]
```

2. A plain `cat -` does not work, because `-` is treated as 'read from standard input'. Prefix the name with `./` so it is read as a file path.

```bash
cat ./-
```

   Output:

```text
bandit1@bandit :~ $ ls
-
bandit1@bandit :~ $ cat ./-
<level-password-redacted>
bandit1@bandit :~ $
```

## Result
Password for Level 2 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 1 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-01.png)

## What I learned
- A filename that looks like a command option needs a path prefix (`./`) for the shell or any other program to treat it as a file.
