# Week 3: Endpoint Logs, Sysmon, auditd and Snort

## LINUX LOGS, SYSMON, AUDITD AND SNORT SETUP

**Program:** DG Interns Hub Cybersecurity Internship 

**Intern:** Chukwu PraiseGod 

**Submission date:** 07 October, 2026

## Summary

This week I worked with endpoint and network detection data in my isolated VMware lab. On Windows, I installed Sysmon with the SwiftOnSecurity config and captured process creation (Event ID 1), network connection (Event ID 3) and file creation (Event ID 11) events. On Ubuntu, I used auditd to record and search commands with `ausearch`, and I built Snort 3 from source to write four detection rules. All four rules fired during tests from Kali, including a rule mapped to MITRE ATT&CK T1046 (Network Service Discovery) that caught an Nmap SYN scan.

I also completed four TryHackMe rooms and three LetsDefend lessons, and wrote ten theory notes and a cheat sheet of 18 entries.

**Main lessons**
- Sysmon only logs what its config allows: a `.txt` file produced no event, but a `.bat` file did.
- Snort 2 rule syntax is not always portable: Snort 3 rejected `threshold`, so I used `detection_filter`.
- Setting `HOME_NET` to a single address kept Kali "external", which the T1046 rule needed.

**Note:** Three LetsDefend lessons (Security Solutions, Network Log Analysis, Incident Response on Linux) need a premium subscription for their labs, so I did not complete them. 

>**All testing was done on machines I own.**

## Folder structure
```
week-03/
├── README.md
├── Notes/            (10 files, one per theory question)
├── Writeups/         (4 TryHackMe rooms, 3 LetsDefend lessons)
├── Findings/         (lab notes and screenshots)
├── Cheat Sheet/      (event ID / rule table)
├── Snort Rules/      (local.rules)
├── Week-3-Report.pdf
└── Week-3-Presentation.pptx
```
## Lab environment
Isolated VMware lab, 192.168.98.0/24: Windows evaluation VM (Sysmon), Ubuntu 26.04 VM (auditd, Snort 3.13.2.0), Kali VM (test traffic). All testing was against my own machines.

## What I did
| Area | Result |
|---|---|
| Sysmon | Installed with the SwiftOnSecurity config. Captured process create (EID 1), network connection (EID 3) and file create (EID 11) events |
| auditd | Installed auditd 4.1.2, added an `execve` rule and a watch rule, searched with `ausearch` |
| Snort | Built Snort 3 from source, wrote 3 starter rules and a T1046 rule. All four fired from Kali tests |
| MITRE ATT&CK | Mapped the Nmap SYN scan rule to T1046 Network Service Discovery |
| Cheat sheet | 18 entries across Windows Security, Sysmon, auditd and Snort |

## Deliverables
| Deliverable | Location |
|---|---|
| Theory notes (Q1 to Q10) | [`Notes/`](/week-3/Notes/) |
| Writeups | [`Writeups/`](/week-3/Writeups/) |
| Screenshots and lab notes | [`Findings/`](/week-3/Findings/) |
| Cheat sheet | [`Cheat Sheet/`](/week-3/cheat-sheet/) |
| Snort rules | [`Snort Rules/local.rules`](/week-3/snort-rules/local.rules) |

## Writeups completed
- **TryHackMe:** Linux Logging for SOC, Intro to Logs, Intro to Log Analysis, Snort.
- **LetsDefend:** How to Investigate a SIEM Alert, SIEM 101, Incident Management 101.
- **Not completed:** Security Solutions, Network Log Analysis and Incident Response on Linux. Their labs and certificates need a premium subscription, and I used free tools only.

## Challenges and lessons
- Sysmon did not log a `.txt` file. The SwiftOnSecurity config only covers certain extensions, and a `.bat` file logged. Telemetry is only as good as the config.
- Snort was not available through apt on Ubuntu 26.04, so I built Snort 3 from source and installed the missing libdnet development package.
- Snort 3 rejected the `threshold` rule keyword, so I used `detection_filter` for the T1046 rule.
- `HOME_NET` was set to the single Ubuntu IP so Kali counted as external; otherwise the T1046 rule could not match.
- Sysmon uses UTC, while auditd and Snort used local time (WAT), so times need aligning when correlating.

## Ethics and safety
All tests ran in an isolated lab on systems I own. Screenshots were checked and blurred where needed. No passwords or flags are included.

## LinkedIn
- Concept post: https://lnkd.in/p/ea22kE9w
- Weekly post: https://lnkd.in/p/eviXVv_D