# OverTheWire Bandit: Level 3 - Level 4

| | |
|---|---|
| **Wargame** | OverTheWire, Bandit |
| **Level** | 3 - 4 |
| **Date completed** | 19/10/2026 |
| **Status** | Completed |

## Goal
The password is stored in a hidden file inside the `inhere` directory.

## Connection
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Enter the password obtained from Level 2. (Not published here, per the internship rules.)

## Steps
1. Move into the `inhere` directory.

```bash
ls
```

```bash
cd inhere
```

2. A normal `ls` and `ls -l` shows nothing. Use `-alsp` to show hidden files (names starting with a dot).

```bash
ls -alsp
```

3. Read the hidden file. 

   Hidden filename: `...Hiding-From-You`

```bash
cat ./...Hiding-From-You
```

   Output:

```text
bandit3@bandit :~ $ ls
inhere
bandit3@bandit :~ $ cd inhere
bandit3@bandit :~ /inhere$ ls
bandit3@bandit :~ /inhere$ ls -l
total 0
bandit3@bandit :~ /inhere$ ls -alsp
total 12
4 drwxr-xr-x 2  root             4096 Jun 24 14:59 ./
4 drwxr-xr-x 3  root             4096 Jun 24 14:59 ../
4 -rw-r ----- 1 bandit4 bandit3    33 Jun 24 14:59 ...Hiding-From-You
bandit3@bandit :~ /inhere$ cat ./ ... Hiding-From-You
<level-password-redacted>
bandit3@bandit :~ /inhere$ |
```

## Result
Password for Level 4 found: `[REDACTED]` (not published, per the rules).

## Screenshot
![Bandit level 3 solved](../Findings/Over%20the%20Wire%20Bandit/bandit-level-03.png)

## What I learned
- Files starting with `.` are hidden from a normal `ls`. `ls -a` shows them.
- Hidden does not mean secure. It only reduces clutter.
