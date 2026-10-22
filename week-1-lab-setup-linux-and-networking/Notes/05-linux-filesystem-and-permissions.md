# Linux File System Hierarchy and File Permissions

## File system hierarchy
Everything in Linux hangs off a single root directory `/`.

| Directory | What it holds | Why it matters in security |
|---|---|---|
| `/` | The root of the whole file system | Starting point of every path |
| `/etc` | System and service configuration files (e.g. `passwd`, `ssh/sshd_config`) | Misconfigurations here are common weaknesses; attackers love reading it |
| `/var/log` | Log files (e.g. `auth.log`, `syslog`) | First place to look when investigating an incident; attackers try to wipe it |
| `/home` | Personal directories of normal users (e.g. `/home/alice`) | Holds user data, SSH keys, shell history |
| `/tmp` | Temporary files, writable by everyone and often cleared on reboot | Attackers often drop tools here because anyone can write to it |
| `/root` | Home directory of the root user | Highly privileged, should not be accessible to others |
| `/bin`, `/usr/bin` | Programs and commands | Where SUID programs like `passwd` live |
| `/dev` | Device files | Represents hardware as files |
| `/proc` | Live information about processes and the kernel | Useful for seeing what is running |

## File permissions
Each file has permissions for three groups: **owner (u)**, **group (g)** and **others (o)**.

| Symbol | Meaning | Number |
|---|---|---|
| `r` | Read | 4 |
| `w` | Write | 2 |
| `x` | Execute (or enter, for a directory) | 1 |

Reading `ls -l` output: `-rwxr-x---  1 alice developers 120 Oct 19 notes.sh`
- `-` = regular file (`d` would be a directory)
- `rwx` = owner can read, write, execute (7)
- `r-x` = group can read and execute (5)
- `---` = others have no access (0) → this file is mode **750**

## chmod: change permissions
| Example | What it does |
|---|---|
| `chmod 750 notes.sh` | Numeric: owner rwx, group r-x, others none |
| `chmod u+x notes.sh` | Symbolic: add execute for the owner |
| `chmod g-w file.txt` | Remove write from the group |
| `chmod o-rwx secret.txt` | Remove all access for others |

## chown: change owner and group
| Example | What it does |
|---|---|
| `sudo chown alice notes.sh` | Make alice the owner |
| `sudo chown alice:developers notes.sh` | Set owner and group |
| `sudo chown -R root:developers /srv/shared` | Change owner and group recursively |

## SUID (Set User ID)
- When a file has the SUID bit, it runs with the **file owner's** privileges rather than the user who launched it.
- Legitimate example: `/usr/bin/passwd` is owned by root with SUID, so a normal user can change their password (which edits protected files).
- Set it with `chmod u+s file` or `chmod 4755 file`. It shows as an `s` in the owner execute position: `-rwsr-xr-x`.
- **Security risk:** a vulnerable or misconfigured SUID program owned by root can be abused for privilege escalation.
- Find SUID files with: `find / -perm -4000 -type f 2>/dev/null`

## Related special bits (used in my lab)
- **SGID** on a directory: new files inherit the directory's group.
- **Sticky bit** on a directory: users can only delete their own files (like `/tmp`).
- My shared folder used `chmod 3770` = SGID + sticky + owner/group full access + others none.

## How this shows up in my lab
- On Ubuntu I created three users (**alice**, **john**, **carol**) and two groups (**developers** and **analysts**). 
- Group membership: **alice:** developers · **john:** developers and analysts · **carol:** analysts only. 
- I created the shared folder `/srv/shared`, owned by `root:developers`, with:
```bash
  sudo chown root:developers /srv/shared
  sudo chmod 3770 /srv/shared
```
- What `3770` means:

| Part | Meaning |
|---|---|
| `3` (special bits) | SGID (new files inherit the `developers` group) plus the sticky bit (users can only delete their own files) |
| `7` (owner) | Read, write, execute |
| `7` (group) | Read, write, execute |
| `0` (others) | No access |

- **Test results:** alice and john (both in `developers`) could create files in `/srv/shared`. **carol**, who is not in `developers`, got **Permission denied** when she tried to list it.
- My admin account is not in `developers` either, so `ls -l /srv/shared` failed with permission denied and I used `sudo ls -la /srv/shared` instead.
- **What I learned:** group membership controls access to a folder, and an account that is not in the group is locked out. Even an administrator needs `sudo` to get in.

### Evidence

![shared folder permission](/Findings/Linux%20Practice/shared-folder-with-correct-permissions-9-commands.png)