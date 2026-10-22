# OverTheWire Bandit: Level 2 - Level 3

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 2 - 3 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is stored in a file called `spaces in this filename` in the home directory.

## Connection
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 1. (Not published here, per the internship rules.)

## Steps
1. List the home directory.

```bash
ls
```

2. Use -- to stop option parsing, and quote the filename so the shell treats it as one argument. 

```bash
cat -- '--spaces in this filename--'
```

   Output:

```text
bandit2@bandit :~ $ cat -- ' -- spaces in this filename -- '
(level-password-redacted)
bandit2@bandit :~ $
```

## Result
Password for Level 3 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 2 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-02.png)

## Challenges
- I tried quoting the text with -- but it returned `error: unexpected argument ....... found`  
- tried using backslash to escape the spaces, which should work but it also returned `error: unexpected argument ....... found` 

## What I learned
- -- tells the command that everything after it is a filename, not an option.
- -- is useful when working with filenames that start with a dash (-) or contains unusual characters.
- The shell splits arguments on spaces, so filenames with spaces must be quoted or escaped.
- Tab completion saves typing and avoids mistakes but may not work in some environment.