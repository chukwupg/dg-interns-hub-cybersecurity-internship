# TryHackMe: Pyramid of Pain

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Pyramid of Pain |
| **Link** | https://tryhackme.com/room/pyramidofpainax |
| **Difficulty** | Easy |
| **Date completed** | 20/10/2026 |
| **Status** | Completed |

## Objective
Understand the Pyramid of Pain and how it ranks indicators of compromise (IoCs) according to the difficulty an adversary faces when changing them.

Learn how defenders can use different indicators to detect malicious activity and increase the cost of an attacker's attempts to evade detection.

## Key Concepts
- Pyramid of Pain and its six levels of adversary disruption
- Indicators of Compromise (IoCs)
- File hashes as identifiers for known malicious files
- IP addresses and domain names used by threat actors
- Host artifacts, including suspicious files, registry entries, and system changes
- Network artifacts, including distinctive traffic patterns and protocol characteristics
- Adversary tools and the challenges of replacing or modifying them
- Tactics, Techniques, and Procedures (TTPs)
- Threat intelligence and detection engineering
- The difference between identifying malicious activity and disrupting an adversary

## Tools and Commands Used
- **VirusTotal:** Checks file hashes, domains, IP addresses, and other indicators against available threat intelligence and security analyses.
- **Shodan:** Helps investigate Internet-exposed infrastructure and services associated with IP addresses.
- **WHOIS:** Retrieves available domain registration information that may help with domain investigations.
- **Network traffic analysis tools:** Tools such as Wireshark and Tshark can help identify suspicious network artifacts and communication patterns, including user-agent.
- **Endpoint security tools:** Can detect host artifacts such as suspicious processes, files, registry changes, and persistence mechanisms.

Example commands for investigating indicators:

```bash
# Calculate a file's SHA-256 hash
sha256sum suspicious_file

#On Windows
Get-FIleHash suspicious_file -Algorithm sha256

# Retrieve DNS records for a domain
dig example.com

# Check registration information for a domain
whois example.com
```

These are representative commands relevant to the room's concepts, not a confirmed record of every command executed during the tasks.

## Summary
Completed the Pyramid of Pain room, which explained how different indicators of compromise affect an adversary's ability to continue operating undetected. The pyramid progresses from hash values, IP addresses, and domain names to host artifacts, network artifacts, tools, and finally Tactics, Techniques, and Procedures (TTPs). Lower-level indicators are generally easier for attackers to change, while higher-level detections can force them to modify tools, techniques, or established operational methods. The practical task involves arranging these IOCs in the correct difficulty order.

## Evidence

![Room Practical](/Findings/TryHackMe/pyramid-of-pain-practical.png)

![THM Room](/Findings/TryHackMe/pyramid-of-pain.png)

## Lessons Learned
- The Pyramid of Pain ranks indicators by the level of difficulty and disruption an adversary experiences when forced to change them.
- Hash values are easy to replace because even a minor file modification can produce a different hash.
- IP addresses and domain names can help identify malicious infrastructure, but attackers may change addresses or register new domains.
- Host artifacts provide additional detection opportunities by revealing traces of malicious activity on compromised systems.
- Network artifacts can expose distinctive communication patterns that remain useful even when an attacker changes infrastructure.
- Detecting adversary tools can be more disruptive because replacing or modifying tools may require additional effort.
- TTPs are at the top of the pyramid because changing established tactics, techniques, and procedures can require substantial operational adjustments.
- Behaviour-based detection can remain effective when attackers change individual indicators such as hashes or IP addresses.
- No single indicator guarantees detection. Combining multiple indicators with contextual analysis improves confidence.
- Effective threat hunting and incident response should focus not only on known malicious indicators but also on the behaviours and techniques behind an attack.

## How this connects to my Week 1 lab
This is blue-team (SOC) thinking, which ties into my notes on SOC analyst vs penetration tester.
