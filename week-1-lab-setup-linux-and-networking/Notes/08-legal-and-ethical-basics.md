# Legal and Ethical Basics

## Core ideas

| Concept | What it means | Why it matters |
|---|---|---|
| **Authorization** | Written permission from the system owner to test their systems | The thing that separates ethical hacking from a crime. Good intentions are not a defence |
| **Scope** | The exact systems, IP ranges, apps and dates you are allowed to test | Testing anything outside scope is unauthorized, even if it is the same company |
| **Rules of Engagement (RoE)** | The agreed rules for the test: what is allowed, when, and how | Protects both the tester and the client |

## What a Rules of Engagement document usually covers
- Targets in scope and explicitly out of scope
- Testing window (dates and times)
- Permitted techniques (e.g. no denial-of-service, no social engineering unless agreed)
- Contact people and an emergency stop procedure
- How data is handled, stored and destroyed
- How findings are reported and kept confidential
- Signed approval from the system owner

## Ethical principles
- **Do no harm:** avoid disrupting systems or exposing real data.
- **Stay in scope** and stop if you are unsure.
- **Confidentiality:** do not share client data or findings with anyone not authorized.
- **Responsible disclosure:** report weaknesses to the owner and give them time to fix them before anything is made public.
- **Honesty:** report what you actually found, including your mistakes.

## The law in Nigeria
- The main law is the **Cybercrimes (Prohibition, Prevention, etc.) Act, 2015**, as amended by the **Cybercrimes (Prohibition, Prevention, etc.) (Amendment) Act, 2024** (signed 28 February 2024).
- Offences it covers include:
  - Unlawful access to a computer
  - Unlawful interception of communications and data
  - Unauthorized modification of computer data
  - System interference
  - Computer-related fraud and forgery
  - Identity theft
  - Cyberstalking
- Personal data handling is also governed by the **Nigeria Data Protection Act, 2023**.
- **Lesson for me:** accessing or probing a system without permission can be a criminal offence in Nigeria. Written authorization and a defined scope are what keep security testing lawful.

## My own lab rules
- I only attack machines I own (my own VMs) on my isolated network.
- I use free tools only.
- I do not scan or test networks or devices I do not own.
