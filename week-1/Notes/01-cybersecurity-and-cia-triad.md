# What is Cybersecurity? The CIA Triad

## What is cybersecurity?
- Cybersecurity is the practice of protecting systems, networks, applications and data from unauthorized access, damage, disruption or theft.
- It rests on three things working together:
  - **People:** awareness, training, clear roles.
  - **Process:** policies, access reviews, incident response plans.
  - **Technology:** firewalls, encryption, antivirus/EDR, monitoring.
- The goal is to keep information and services trustworthy and available while reducing both the chance and the impact of attacks.
- Main areas: network security, application security, endpoint security, cloud security, identity and access management, and incident response.
- It matters because almost every organization, from banks to hospitals, depends on digital systems. A breach can cost money, trust and even safety.

## The CIA triad
The CIA triad is a model for thinking about what we are trying to protect. Every security control supports at least one of its three parts.

| Pillar | What it means | Real-world example | What a failure looks like | Common controls |
|---|---|---|---|---|
| **Confidentiality** | Only authorized people can see the information | Your bank PIN and OTP should be known only to you and the bank | An attacker phishes your OTP and reads your account details | Encryption, access control, MFA, strong passwords |
| **Integrity** | Information stays accurate and is not changed without permission | A transfer of ₦5,000 must arrive as ₦5,000, not ₦50,000 | Data is altered in transit or a record is tampered with | Hashing, digital signatures, checksums, audit logs, input validation |
| **Availability** | Systems and data are accessible when needed | A bank app must work on salary day | A DDoS attack or ransomware takes the service offline | Backups, redundancy, DDoS protection, patching, disaster recovery |

## Key points to remember
- The three goals can pull against each other. For example, very strict access controls improve confidentiality but can reduce availability.
- Real incidents often break more than one pillar. Ransomware hits availability (files locked) and confidentiality (data stolen) at the same time.
- A useful question for any control: *which of C, I or A does this protect?*

## How this shows up in my lab
- **Confidentiality:** my shared folder uses chmod 3770, so users outside the developers group cannot read it. 
- **Integrity:** file ownership and permissions stop other users editing files they do not own.
- **Availability:** VM snapshots let me restore a clean machine quickly.
