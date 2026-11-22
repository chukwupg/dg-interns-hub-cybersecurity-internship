# Q6. MITRE ATT&CK vs the Cyber Kill Chain

## Goal
Explain how ATT&CK is structured, compare it with the Cyber Kill Chain, and map 5 attacks from Weeks 2-4.

## ATT&CK structure
- **Tactics:** the attacker's goal at a stage (the "why"), such as Discovery, Persistence or Credential Access.
- **Techniques:** how the goal is achieved (the "how"), such as T1046 Network Service Discovery.
- **Sub-techniques:** a more specific version of a technique, such as T1059.001 PowerShell (under T1059 Command and Scripting Interpreter).
- Each technique page also lists procedures (real examples), mitigations and detection ideas.
- ATT&CK matrices cover different environments (Enterprise, Mobile, ICS). Enterprise is the one I use.

## Cyber Kill Chain (Lockheed Martin) phases
1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control (C2)
7. Actions on Objectives

## ATT&CK vs Kill Chain

| | Cyber Kill Chain | MITRE ATT&CK |
|---|---|---|
| Model | Linear sequence of phases | Matrix of tactics and techniques (not strictly ordered) |
| Detail | High level | Very detailed, specific techniques |
| Focus | Stopping an intrusion early | Describing and detecting attacker behaviour |
| Strength | Simple, good for explaining an attack story | Good for detection engineering, gap analysis and threat intel |
| Weakness | Weak after initial compromise; assumes a fixed order | Large and needs more effort to use well |
| Used together | Kill Chain gives the story; ATT&CK gives the technique detail | |

## Attacks from Weeks 2-4 mapped

| Attack observed | Week | Kill Chain phase | ATT&CK technique |
|---|---|---|---|
| Nmap SYN scan from Kali against Ubuntu and Windows VMs | 2, 3, 4 | Reconnaissance | T1046 Network Service Discovery |
| Hydra SSH brute force from Kali against Ubuntu user `bob` | 4 | Exploitation | T1110.001 Brute Force: Password Guessing |
| Repeated failed Windows logons using non-existent accounts (Event ID 4625) | 2 | Exploitation | T1110 Brute Force |
| Service created with `sc.exe create` pointing to notepad.exe | 2 | Installation | T1543.003 Create or Modify System Process: Windows Service |
| New local user `labtest` created on Windows | 2 | Installation | T1136.001 Create Account: Local Account |

Check the IDs on the ATT&CK website before submitting, since names and numbering can be updated.

## How this shows up in my lab
- Detection sources: Snort rule for T1046 (Week 3), Splunk `linux_secure` logs and my "SSH Bruteforce" alert (Week 4), Windows Security events 4625 and 4720/4624, and Sysmon.
- These techniques go into my ATT&CK Navigator layer with the Week 5 Atomic tests (T1059.001, T1136.001, T1053.005): [Navigator layer](../Findings/attack-navigator/attack-layer-weeks2-5.svg)