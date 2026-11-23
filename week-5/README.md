# Week 5: Phishing, Malware Triage, Threat Intelligence and Incident Response

**Program:** DG Interns Hub Cybersecurity Internship

**Intern:** Chukwu PraiseGod 

**Date:** 22 November, 2026

## Summary
This week I investigated email and endpoint threats the way a Tier 1 or Tier 2 analyst would. I analysed three public phishing emails, read two public sandbox reports, tested an EICAR file on my Windows VM, mapped techniques from Weeks 2 to 5 in ATT&CK Navigator, and ran three Atomic Red Team tests to see what my Sysmon and Splunk setup would catch. I wrote an incident report on the Atomic tests. The main finding was that my SIEM alerted on one of the three techniques, and the other two exposed gaps in logging and rules.

All testing was done in my isolated lab (192.168.98.0/24) on systems I own. No live malware was used and no links or attachments from the phishing samples were opened.

## Folder structure

```
week-05-phishing-malware-ir/
├── README.md
├── Week5-Report.pdf
├── Week5-Presentation.pptx
├── Notes/
│   ├── q1-incident-response-lifecycle.md
│   ├── q2-phishing-types-and-red-flags.md
│   ├── q3-spf-dkim-dmarc.md
│   ├── q4-reading-email-headers.md
│   ├── q5-ioc-vs-ioa-pyramid-of-pain.md
│   ├── q6-attack-vs-kill-chain.md
│   ├── q7-static-vs-dynamic-analysis.md
│   └── q8-incident-reports-and-severity.md
├── Writeups/
│   ├── thm-cyber-kill-chain.md
│   ├── thm-pyramid-of-pain.md
│   ├── thm-phishing-analysis-fundamentals.md
│   ├── thm-intro-to-cyber-threat-intel.md
│   └── thm-threat-intelligence-tools.md
├── Findings/
│   ├── phishing-analysis/
|       └── emails-and-triage-script/
│   ├── safe-malware-triage/
│   │   └── sandbox-report/
│   ├── attack-navigator/
│   └── atomic-red-team/
├── Incident Report/
│   └── Week5-Incident-Report.pdf
└── Cheat Sheet/
    ├── ioc-type-where-to-find-it-tool-to-check-it.md
    └── phishing-red-flag-checklist.md
```

## Deliverables

| Deliverable | Location | Status |
|---|---|---|
| Theory notes (8 files) | [Notes](Notes/) | Complete |
| TryHackMe writeups (5 rooms) | [Writeups](Writeups/) | Complete |
| Phishing analysis (3 samples) | [Findings/phishing-analysis](Findings/phishing-analysis/) | Complete |
| EICAR triage and 2 sandbox reports | [Findings/safe-malware-triage](Findings/safe-malware-triage/) | Complete |
| ATT&CK Navigator layer (JSON, SVG, PNG) | [Findings/attack-navigator](Findings/attack-navigator/) | Complete |
| Atomic Red Team tests (3) | [Findings/Atomic](Findings/atomic-red-team/) | Complete |
| Incident report (2 to 3 pages) | [Incident Report](/week-5/incident-report/Week5-Incident-Report.pdf) | Complete |
| Cheat sheets (2) | [Cheat Sheet](/week-5/cheat-sheet/) | Complete |
| PDF report | [Week5-Report.pdf](Week5-Report.pdf) | Complete |
| Presentation (7 slides) | [Week5-Presentation.pptx](Week5-Presentation.pptx) | Complete |

## Theory notes

| File | Question |
|---|---|
| q1 | Incident response lifecycle (NIST SP 800-61) with a table of actions per phase |
| q2 | Phishing types and a red-flag checklist |
| q3 | SPF, DKIM and DMARC with a pass and a fail example |
| q4 | How to read an email header |
| q5 | IOC vs IOA and the Pyramid of Pain |
| q6 | MITRE ATT&CK vs the Cyber Kill Chain, with five attacks from Weeks 2 to 4 mapped |
| q7 | Static vs dynamic malware analysis, sandboxes and safety rules |
| q8 | Incident report contents, severity levels, escalation and a report template |

**Link:** [Notes](/week-5/Notes/)

## TryHackMe rooms

| Room | Type | Writeup |
|---|---|---|
| Cyber Kill Chain | Core | [thm-cyber-kill-chain.md](Writeups/thm-cyber-kill-chain.md) |
| Pyramid of Pain | Core | [thm-pyramid-of-pain.md](Writeups/thm-pyramid-of-pain.md) |
| Phishing Analysis Fundamentals | Core | [thm-phishing-analysis-fundamentals.md](Writeups/thm-phishing-analysis-fundamentals.md) |
| Intro to Cyber Threat Intel | Core | [thm-intro-to-cyber-threat-intel.md](Writeups/thm-intro-to-cyber-threat-intel.md) |
| Threat Intelligence Tools | Optional | [thm-threat-intelligence-tools.md](Writeups/thm-threat-intelligence-tools.md) |

The MITRE room (core) and the Yara room (optional) require a premium subscription, so I did not complete them.

## Hands-on tasks

### 1. Phishing analysis
Three public samples from the phishing_pot repository. I read the headers as text in a Kali VM with a small Python script (`triage.py`), listed URLs without opening them, hashed attachments and checked reputation with free tools.

| Sample | Lure | Verdict | Key evidence |
|---|---|---|---|
| sample-10 | Fake OKX Chrome extension notice | Malicious | OKX display name on an unrelated domain; SPF none, DKIM fail; look-alike extension name; reputation tools were clean |
| sample-10002 | French "CPF" account update | Malicious (moderate) | Bing redirect to linklift[.]space (2/92 on VirusTotal); no authentication at the final hop |
| sample-10010 | "Payment could be returned" with a PDF | Suspicious (moderate) | All authentication passed via Amazon SES; Reply-To domain unregistered; malformed PDF with no payload |

### 2. Safe malware triage
- **EICAR:** dropped on the Windows VM, detected by Defender, with Sysmon and Splunk checked for evidence.
- **Public ANY.RUN reports:** `app.exe` (Glupteba) and `Client1.exe` (XWorm). For each I noted the process tree, network indicators, ATT&CK techniques and behaviour such as persistence. I did not download or run either sample.

Folder: [safe-malware-triage](/week-5/Findings/safe-malware-triage/)

### 3. ATT&CK Navigator layer
A layer for the techniques seen in Weeks 2 to 5: T1046, T1110.001, T1136.001, T1543.003, T1059.001, T1566.001, T1566.002 and T1656. Each technique has a note on the week it was observed and the log source or detection that captured it. Files: JSON, SVG and PNG.

Folder: [attack-navigator](/week-5/Findings/attack-navigator/)

### 4. Atomic Red Team
Run on the Windows VM after taking a snapshot. Evidence came from Sysmon and Splunk.

| Technique | Atomic test | Evidence | Alert fired |
|---|---|---|---|
| T1059.001 PowerShell | Test 17, PowerShell Command Execution | Sysmon EID 1: `powershell.exe -e` with an encoded command | No |
| T1136.001 Local account | Account creation test | Security Event 4720 | Yes ("New User Created") |
| T1053.005 Scheduled task | Scheduled task test | No Event 4698, because auditing was off | No |

Folder: [atomic-red-team](/week-5/Findings/atomic-red-team/)

### 5. Incident report
A 2 to 3 page report on the Atomic tests (a lab simulation), with a timeline, indicators, ATT&CK mapping, severity (Medium, with justification), containment actions and recommendations.

### 6. Cheat sheets
- A table of 12 IOC types, where to find each and which free tool checks it.
- A one-page phishing red-flag checklist.

Folder: [cheat-sheet](/week-5/cheat-sheet/)

## Key findings and detection gaps
- **No alert for encoded PowerShell.** A Sysmon search for `powershell.exe` with `-e` matched my test and can become a rule.
- **Scheduled task creation was not audited.** "Other Object Access Events" auditing was off, so Event 4698 was never logged.
- **PowerShell script block logging and Defender logs are not forwarded to Splunk.**
- **Clean reputation does not mean safe.** Sample 1 looked clean on most tools but was still phishing.
- **Passing SPF, DKIM and DMARC does not mean safe.** Sample 3 passed all of them through Amazon SES.
- **An alert is only trusted once it is tested.** My "New User Created" alert from Week 4 was first tested this week, and it worked.

## Tools used (all free)
VirusTotal, urlscan.io, AbuseIPDB, AlienVault OTX, MXToolbox, CyberChef, public ANY.RUN reports, MITRE ATT&CK Navigator, Atomic Red Team, Sysmon, Splunk, Microsoft Defender, VMware Workstation, Kali Linux and Python 3.

## Not completed
- TryHackMe MITRE and Yara rooms: premium only.
- CyberDefenders or Blue Team Labs Online challenge: skipped because of the submission deadline (Planned).

## Safety and ethics
- Testing was limited to my own isolated lab. Nothing was run against systems I do not own.
- No live malware was downloaded or executed. Only the EICAR test file and public sandbox reports were used.
- Phishing samples were read as text. No links were opened and no attachments were run.
- Indicators are defanged in all write-ups.
- Screenshots were checked for sensitive information before publishing. No passwords, flags or room answers are included.

## LinkedIn
- Concept post, "How to spot a phishing email using headers": [[link]]
- Weekly post (incident report summary and ATT&CK Navigator screenshot, tagging DG Interns Hub): https://lnkd.in/p/eK8Zs4Yz