# Q9: Key Linux log files for a SOC analyst

| Log file path | Purpose | Common events |
|---|---|---|
| `/var/log/auth.log` | Authentication and authorisation | SSH logins, failed passwords, `sudo` use, new users |
| `/var/log/syslog` | General system activity | Service start/stop, cron jobs, network and daemon messages |
| `/var/log/audit/audit.log` | Detailed kernel audit records (auditd) | Command execution (EXECVE), file access, logins, rule changes |
| `/var/log/kern.log` | Kernel messages | Driver and hardware errors, firewall drops, USB devices |
| `/var/log/apache2/access.log` | Web requests to Apache | Source IP, URL, status code, user agent, scans and attacks |
| `/var/log/apache2/error.log` | Apache errors | Failed requests, misconfigurations, exploit attempts |
| `/var/log/dpkg.log` | Package installs and removals | Software installed or removed |
| `/var/log/wtmp` and `/var/log/btmp` | Login history (binary files) | Successful (`last`) and failed (`sudo lastb`) logins |

## Handy commands
| Command | Use |
|---|---|
| `sudo tail -f /var/log/auth.log` | Watch authentication live |
| `sudo grep "Failed password" /var/log/auth.log` | Find failed SSH logins |
| `sudo ausearch -m EXECVE -i` | Read audit command records |
| `journalctl -u ssh` | Service logs from journald |

## Why these matter
- `auth.log`: brute force and privilege abuse.
- `audit.log`: who ran what, with arguments.
- `access.log`: web attacks and reconnaissance.
- Forward them to a SIEM so they are searchable and correlated.

## How this shows up in my lab
- `/var/log/audit/audit.log` is where my `ausearch` results came from (EXECVE and CONFIG_CHANGE records).
- Snort alerts printed to the console during my tests. They were not written to a file in my setup.
- Snort saw the HTTP traffic to port 8000 because it inspects packets. 