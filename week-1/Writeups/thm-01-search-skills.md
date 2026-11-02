# TryHackMe: Search Skills

| | |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Search Skills |
| **Link** | https://tryhackme.com/room/searchskillscS |
| **Difficulty** | Easy |
| **Date completed** | 17/10/2026 |
| **Status** | Completed |

## Objective
Learn how to efficiently search the Internet and use specialised cybersecurity services, vulnerability databases, technical documentation, and code repositories to gather information during security investigations and assessments.

## Key Concepts
- Search engine techniques and effective information gathering
- Shodan for discovering Internet-connected devices and exposed services
- VirusTotal for analysing suspicious files, URLs, domains, and IP addresses
- Common Vulnerabilities and Exposures (CVE) identifiers and vulnerability databases (NVD, Exploit-DB)
- Linux manual pages (`man`) for understanding commands and their options
- GitHub for finding source code, scripts, tools, and technical references

## Tools and Commands Used
- **Shodan:** Search for Internet-connected devices, exposed ports, services, and associated metadata.
- **VirusTotal:** Investigate suspicious URLs, file hashes, domains, and IP addresses using community and security vendor analysis.
- **CVE databases:** Research publicly documented vulnerabilities using their CVE identifiers, descriptions, and available technical details.
- **`man`:** Access local Linux manual pages to understand command syntax, options, and usage.

Example:
```bash
man nmap
```

- **GitHub:** Search repositories, source code, security tools, and documentation relevant to cybersecurity research.

## Summary
Completed the Search Skills room with 100% progress, covering different ways to find and verify technical information during cybersecurity activities. The exercises introduced Shodan for discovering exposed Internet-connected assets, VirusTotal for investigating potentially malicious indicators, CVE databases for researching known vulnerabilities, Proof of Concepts (PoCs) from websites like Exploit-DB used to demonstrate the vulnerability.Linux manual pages for understanding command usage, and GitHub for locating source code and security tools. The room demonstrated the importance of using specialised search services and reliable technical references to support reconnaissance, threat intelligence, vulnerability research, and troubleshooting.

## Evidence 

![THM search skills proof of completion](/Findings/TryHackMe/search-skills.png)

## Lessons Learned
- Effective cybersecurity research requires knowing where to search, not just how to use a general search engine.
- Shodan can help identify exposed services and technologies that may require further security investigation.
- VirusTotal provides useful threat intelligence by aggregating analysis from multiple security engines and other sources, but its results require careful interpretation.
- CVE identifiers provide a standard way to reference and research publicly disclosed vulnerabilities.
- Linux manual pages are valuable references for understanding command syntax, available options, and correct usage.
- GitHub can provide practical examples, scripts, and security tools, but repositories should be assessed for credibility and safety before use.
- Findings from online security services should be verified against authoritative sources and relevant technical documentation.

