# TryHackMe: Linux Fundamentals Part 1

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Linux Fundamentals Part 1 |
| **Link** | https://tryhackme.com/room/linuxfundamentalspart1 |
| **Difficulty** | Easy |
| **Date completed** | 18/10/2026 |
| **Status** | Completed |

## Objective
Learn the essential Linux terminal commands for identifying the current user, navigating the filesystem, viewing file contents, searching for files and text, and combining commands using shell operators.

## Key Concepts
- Linux command-line interface and shell interaction
- User identification with `whoami`
- Displaying text with `echo`
- Filesystem navigation using `pwd`, `ls`, and `cd`
- Reading files with `cat`
- Searching for files and directories with `find`
- Searching file contents with `grep`
- Shell operators for combining commands and controlling command execution

## Tools and Commands Used
- `whoami`: Displays the username of the currently logged-in user.
- `echo`: Prints text or variable values to the terminal.
- `pwd`: Displays the full path of the current working directory.
- `ls`: Lists files and directories in a location.
- `cd`: Changes the current working directory.
- `cat`: Displays the contents of a file.
- `find`: Searches for files and directories based on specified criteria.
- `grep`: Searches text for lines matching a specified pattern.

Example commands:

```bash
whoami
echo "Hello Linux"
pwd
ls
cd /home
cat example.txt
find /home -name "example.txt"
grep "error" logfile.txt
```

Common shell operators:

- `;` runs commands sequentially, regardless of whether the previous command succeeds.
- `&&` runs the next command only if the previous command succeeds.
- `||` runs the next command only if the previous command fails.
- `|` passes the output of one command to another command as input.

Examples:

```bash
pwd && ls
whoami; pwd
cat logfile.txt 
grep "THM" access.log
```

## Summary
Completed the Linux Fundamentals (Pt1) room with 100% progress. The room introduced essential Linux terminal commands for interacting with the operating system, identifying the current user, navigating directories, listing files, and reading file contents. It also covered searching for files with `find`, locating specific text with `grep`, and using shell operators to combine commands and control execution. These fundamentals provide a foundation for working efficiently in Linux environments commonly used for cybersecurity investigations, system administration, and penetration testing.

## Evidence 

![THM room](/Findings/TryHackMe/linux-fundamentals.png)

## Lessons Learned
- The terminal provides direct access to Linux system functions without requiring a graphical interface.
- Commands such as `whoami` and `pwd` help establish the current user context and working directory before performing tasks.
- Understanding filesystem navigation with `ls` and `cd` makes it easier to locate and manage files.
- The `find` command searches for files and directories, while `grep` searches text for matching patterns.
- Shell operators allow multiple commands to be combined into efficient workflows.
- The `&&` and `||` operators support conditional command execution based on success or failure.
- The pipe operator `|` enables command output to be processed by another command, which is particularly useful for filtering and analysing information.
- Familiarity with Linux commands is an important foundation for cybersecurity tasks such as reconnaissance, log analysis, and system enumeration.

## How this connects to my Week 1 lab
These are the same commands I used in my Ubuntu practice (users, groups, find, grep) and in Bandit levels 0 to 10.
