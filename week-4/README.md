# Week 4: SIEM in Practice: Splunk, Wazuh and Log Ingestion

**Program:** DG Interns Hub Cybersecurity Internship 

**Intern:** Chukwu PraiseGod 

**Submission date:** 15 November, 2026

## Summary

This week I built a working SIEM pipeline end to end using Splunk, on a dedicated headless Ubuntu Server VM in my isolated 192.168.98.0/24 lab. I installed the Universal Forwarder on both my Windows VM (Security + Sysmon logs) and Ubuntu VM (`/var/log/auth.log`), and confirmed all three sources landing in the `lab` index.

To test the pipeline against real activity rather than just theory, I ran my own SSH brute-force attack with Hydra (rockyou wordlist) and an Nmap SYN scan from Kali against my own Ubuntu VM. The Hydra attack was fully captured and traced through to a working alert; the Nmap scan produced no matching log entry, which I documented as a real visibility gap rather than a failure - host logs alone don't see network-level recon.

From there I wrote 5 SPL detections and tested each one by running it against real log data in my lab. I saved 2 as scheduled alerts ("SSH Bruteforce", "New User Created") and built a 4-panel dashboard. Both alerts are configured correctly. I verified the underlying search logic, not the live alerting mechanism.

Wazuh was not installed this week due to an 8GB RAM constraint on my host (Splunk plus my Windows VM already fill it). The brief allows building one SIEM fully and documenting the other, so I researched Wazuh's architecture and wrote a custom correlation rule (mapped to MITRE T1110) without running it live, this is flagged clearly wherever Wazuh is referenced, rather than presented as tested work.

## Folder structure

```
week-03/
├── Notes/           (8 files, one per theory question (Q1-Q8))
├── Writeups/        (2 TryHackMe room writeups)
├── Findings/        (screenshots + 3 triage notes)
├── Detections/      (5 SPL searches + custom Wazuh rule)
├── Cheat Sheet/     (SPL command table + SIEM alert table)
├── Week4-Report.pdf
├── Week4-Presentation.pptx
└── README.md        (this file)
```

## What I built
- **Splunk Enterprise 10.6.1.1** on a dedicated headless Ubuntu Server VM (192.168.98.x) in my isolated lab, with a `lab` index.
- **Log ingestion:** Splunk Universal Forwarder on my Windows VM (Security + Sysmon logs) and my Ubuntu VM (`/var/log/auth.log`), all confirmed flowing into `index=lab`.
- **Attack-to-alert:** Hydra SSH brute force (rockyou wordlist, first 20 entries) and an Nmap `-sS` scan, both run from Kali against my own Ubuntu VM - found and documented in Splunk.
- **5 SPL detections** covering Windows failed logons (4625), PowerShell execution (Sysmon EID 1), new user creation (4720), SSH brute force, and rare parent-child process pairs.
- **2 scheduled alerts** ("SSH Bruteforce", "New User Created") and a **4-panel dashboard**.
- **Custom Wazuh rule** (ID 100010, MITRE T1110) written and documented, but **not installed or tested** this week.

## Scope decision: Splunk fully built, Wazuh documented only
My lab PC has 8 GB RAM. Splunk alone needs ~4 GB and my Windows VM needs 4 GB, which already fills the host. Wazuh needs another 4-8 GB on top of that. 

The brief explicitly allows building one SIEM fully and documenting the other tool's room/theory only, so I built Splunk end-to-end and wrote the Wazuh architecture notes (Q4) and the custom rule (Detections folder) from research rather than a live install. This is stated plainly wherever Wazuh is referenced.

## Lab environment
- VMware Workstation Pro, isolated network 192.168.98.0/24
- Ubuntu (log source + Splunk forwarder): 192.168.98.129
- Kali (attacker): 192.168.98.130
- Windows evaluation VM (log source): 192.168.98.131
- Splunk server: dedicated headless Ubuntu Server VM

## LinkedIn
- Concept post: "Why logs alone are not enough: what a SIEM adds"

    Link: https://lnkd.in/p/erjUeQTV

- Weekly post: dashboard screenshot + SSH brute-force detection, tagging DG Interns Hub 
    
    Link: https://lnkd.in/p/e2SesuJN

## What I'd do with more time/RAM
- Install Wazuh and actually test the custom rule with `wazuh-logtest`.
- Add a slow/low-and-slow brute-force detection (current threshold would miss an attacker staying under 5 attempts per 5 minutes).
- Feed Snort/network data into Splunk to catch recon (my Nmap scan produced no log entry this week - a real visibility gap, documented in Triage Note 3).