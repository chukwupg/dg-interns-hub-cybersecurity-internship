# Cheat Sheet: Linux Commands - What It Does and When to Use It

30 entries. 

| # | Linux Command | What It Does | When to Use It |
|---|---|---|---|
| 1 | `pwd` | Prints the current working directory | When you are lost and need to know where you are |
| 2 | `ls` | Lists files and folders | To see what is in a directory |
| 3 | `cd <dir>` | Changes directory | To move around the file system; `cd ..` goes up, `cd ~` goes home |
| 4 | `mkdir <name>` | Creates a directory | To set up folders for a project or shared space |
| 5 | `cp <src> <dest>` | Copies files or directories (`-r` for folders) | To make a backup before editing a config file |
| 6 | `mv <src> <dest>` | Moves or renames files | To rename a file or move it to another folder |
| 7 | `rm <file>` | Deletes a file (`-r` for folders) | To remove files you no longer need. There is no recycle bin, so be careful |
| 8 | `cat <file>` | Prints a file's contents | To read short files, such as a password file in Bandit |
| 9 | `grep <pattern> <file>` | Searches for text inside files | To find a keyword in logs or data (Bandit level 7) |
| 10 | `grep -r <pattern> <dir>` | Searches recursively through a directory | To find a setting across many config files |
| 11 | `find <path> -name <pattern>` | Finds files by name, size, owner or permission | To locate a file, or to hunt for SUID files with `-perm -4000` |
| 12 | `chmod <mode> <file>` | Changes file permissions | To control who can read, write or execute a file, e.g. `chmod 750 script.sh` |
| 13 | `chown <user:group> <file>` | Changes the owner and group of a file | To fix ownership, or set up a shared folder |
| 14 | `whoami` | Shows the current user | To confirm which account you are using |
| 15 | `sudo <command>` | Runs a command with administrator (root) rights | When a task needs elevated privileges, such as installing software |
| 16 | `adduser <name>` | Creates a new user with a home directory | When setting up accounts, such as my 3 lab users |
| 17 | `passwd <user>` | Changes a user's password | To set or reset a password |
| 18 | `groupadd <name>` | Creates a new group | To organize users who need shared access |
| 19 | `usermod -aG <group> <user>` | Adds a user to a group without removing existing groups | To give a user access to a shared folder |
| 20 | `ip a` | Shows network interfaces, IP and MAC addresses | To find a VM's IP address |
| 21 | `ping -c 4 <host>` | Sends 4 ICMP echo requests | To test whether another machine is reachable |
| 22 | `traceroute <host>` | Shows the path packets take to a destination | To see each hop and find where connectivity breaks |
| 23 | `nslookup <domain>` | Looks up a domain's IP address | For a quick DNS check |
| 24 | `dig <domain>` | Detailed DNS query tool | To see record types, TTLs and which server answered |
| 25 | `crontab -e` | Edits your scheduled jobs (cron) | To run a task automatically on a schedule |
| 26 | `crontab -l` | Lists your scheduled jobs | To confirm a cron job is installed |
| 27 | `systemctl status <service>` | Shows whether a service is running | To check services like cron or ssh |
| 28 | `history` | Lists previously typed commands | To review or reuse commands, and to document your work |
| 29 | `apt update && apt upgrade` | Refreshes the package list and installs updates (Ubuntu/Kali) | To keep a system patched |
| 30 | `script -a <file>` | Records everything typed and printed in the terminal to a file | To capture proof of your commands and output |
