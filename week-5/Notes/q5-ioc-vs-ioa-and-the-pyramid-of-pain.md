# Q5. IOC vs IOA and the Pyramid of Pain

## Goal
Explain the difference between IOCs and IOAs, and how hard each artifact is for an attacker to change.

## IOC vs IOA

| | IOC (Indicator of Compromise) | IOA (Indicator of Attack) |
|---|---|---|
| Meaning | Evidence that a compromise already happened or is known | Evidence of attacker behaviour or intent, as it happens |
| Focus | Artifacts: what was left behind | Actions: what the attacker is doing |
| Examples | File hash, malicious IP or domain, URL, registry key, filename | Port scan pattern, PowerShell downloading a file, many failed logins then a success, new service creation |
| Timing | Often after the fact; reactive | Can be real time; proactive |
| Weakness | Attackers change them easily, so they go stale | Needs context and tuning; can give false positives |
| Typical use | Blocklists, threat intel feeds, IOC searches | Behaviour-based detection rules, hunting |

## Pyramid of Pain
Created by David Bianco. It shows how much pain it causes the attacker when defenders detect and block each type of indicator. Higher level means more pain.

| Level (bottom to top) | Example | Difficulty for attacker to change | Value to defender |
|---|---|---|---|
| Hash values | File SHA256 | **Trivial.** Change one byte | Very low; precise but short-lived |
| IP addresses | C2 server IP | **Easy.** Use a new server or proxy | Low |
| Domain names | Phishing domain | **Simple.** Register a new domain (costs money and time) | Low to medium |
| Network and host artifacts | User-Agent string, registry key, URL pattern, mutex | **Annoying.** Must change tooling or config | Medium |
| Tools | Malware family, password cracker, attack framework | **Challenging.** Must find or build new tools | High |
| TTPs (tactics, techniques and procedures) | Credential dumping, phishing then PowerShell, lateral movement style | **Tough.** Must change how they operate | Very high |

## Key points
- Detecting at the top forces the attacker to change behaviour, not just swap an indicator.
- Good defence uses both: IOCs for quick wins, IOAs/TTPs for lasting detection.
- ATT&CK techniques sit at the TTP level.

## How this shows up in my lab
- **Hash level:** the EICAR file hash is a hash IOC, and an antivirus blocks it by signature: [[Defender detection screenshot]]
- **IP level:** the Kali attacker IP 192.168.98.130 appears in my Splunk results for the Hydra and Nmap tests.
- **Behaviour level (IOA/TTP):** my Snort rule for Nmap SYN scans and my SPL search for repeated SSH failures detect behaviour, not a specific IP or file.
- Phishing sample IOCs (defanged URLs, domains, hashes): [[IOC table from my incident report]]