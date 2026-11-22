# Q1. Incident Response Lifecycle (NIST SP 800-61)

## Goal
Explain the four-phase incident response (IR) lifecycle and list the actions in each phase.

## The four phases
1. Preparation
2. Detection and Analysis
3. Containment, Eradication and Recovery
4. Post-Incident Activity

The model is a loop: lessons from phase 4 feed back into phase 1.

## Actions in each phase

| Phase | Purpose | Key actions | Example output |
|---|---|---|---|
| 1. Preparation | Be ready before anything happens | Write an IR plan and playbooks; set up logging (Sysmon, auditd, SIEM); define roles and contacts; prepare tools and clean jump boxes; train staff; run phishing awareness | IR plan, contact list, log sources onboarded |
| 2. Detection and Analysis | Spot an incident and decide if it is real | Monitor alerts; triage and validate (true or false positive); collect evidence; scope affected hosts and accounts; extract IOCs; map to ATT&CK; assign severity; open a ticket | Triage notes, IOC list, severity rating |
| 3. Containment, Eradication and Recovery | Stop the damage, remove the threat, restore service | **Contain:** isolate host, disable account, block IP or domain. **Eradicate:** remove malware, close the entry point, reset credentials, patch. **Recover:** restore from clean backup, return to service, monitor for reoccurrence | Containment log, clean system, monitoring in place |
| 4. Post-Incident Activity | Learn and improve | Lessons-learned meeting; final incident report; update detections and playbooks; fix gaps; share IOCs; track metrics (time to detect, time to respond) | Final report, new detection rules, updated playbook |

## Key points
- Evidence handling matters from phase 2: record what you did, when, and keep original data unchanged.
- Containment choices balance stopping the attacker against keeping the business running and preserving evidence.
- Not every alert becomes an incident. Phase 2 decides that.

## Note on the newer NIST version
- NIST published SP 800-61 Revision 3 in April 2025. It replaces Revision 2.
- Rev 3 ties incident response to the six CSF 2.0 functions (Govern, Identify, Protect, Detect, Respond, Recover) instead of the four-phase diagram.
- The four-phase model is still widely taught, and the underlying work is the same.

## How this shows up in my lab
- **Preparation:** Sysmon on the Windows VM (192.168.98.131), auditd on Ubuntu (192.168.98.129), and Splunk with the `lab` index collecting logs.
- **Detection and Analysis:** my Splunk alerts "SSH Bruteforce" and "New User Created", and the SPL searches I wrote in Week 4.
- **Containment (practice):** isolate the Windows VM, disable the test account. 
- **Post-incident:** [[detection gaps found during the Atomic tests and what I will change]]