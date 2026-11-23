# IOC Type - Where to Find It - Tool to Check It

**Week 5 | Cheat Sheet | Folder: Cheat Sheet**

All tools listed are free. Check an indicator in more than one source, because one clean result never proves it is safe.

| # | IOC type | Where to find it | Tool to check it |
|---|---|---|---|
| 1 | **File hash** (MD5, SHA1, SHA256) | Attachment hashed with `sha256sum` or `Get-FileHash`; Sysmon EID 1 `Hashes` field; Defender detection details; header of a sandbox report | VirusTotal (search by hash, do not upload private files); MalwareBazaar; Hybrid Analysis; AlienVault OTX |
| 2 | **IP address** | Email `Received` lines and `X-Originating-IP`; firewall and proxy logs; Sysmon EID 3; Linux `auth.log` source address; sandbox network tab | AbuseIPDB; VirusTotal; AlienVault OTX; Cisco Talos Intelligence |
| 3 | **Domain name** | Links in the email body; sender and Reply-To domains; DNS logs; Sysmon EID 22; sandbox DNS tab | VirusTotal; AlienVault OTX; urlscan.io; whois lookup; Cisco Talos Intelligence |
| 4 | **URL** | The real `href` in the email HTML (hover, do not click); proxy logs; sandbox HTTP requests | urlscan.io (search first, scan as Unlisted); VirusTotal URL search; URLhaus |
| 5 | **Email address** (From, Return-Path, Reply-To) | Raw message headers (`.eml` or "Show original") | MXToolbox (SPF, DKIM and DMARC records of its domain); whois; VirusTotal (domain) |
| 6 | **Email header values** (Message-ID, Received chain, Authentication-Results) | Raw message headers | MXToolbox Email Header Analyzer; manual reading bottom to top; AbuseIPDB for the origin IP |
| 7 | **File name and path** | Attachment name; Sysmon EID 11 (file created); Defender detection; sandbox dropped files | Splunk search over Sysmon; ANY.RUN or Hybrid Analysis reports; MalwareBazaar (search by file name) |
| 8 | **Registry key or value** (persistence) | Sysmon EID 12, 13 and 14; Registry Editor; sandbox registry activity | Splunk search over Sysmon; Sysinternals Autoruns; ANY.RUN or Hybrid Analysis reports |
| 9 | **Process and command line** | Sysmon EID 1; Security 4688 if command-line auditing is on; auditd `EXECVE` on Linux | Splunk search; CyberChef (decode base64 from `-e` or `-enc`); VirusTotal for the binary's hash |
| 10 | **Account, scheduled task or service name** | Security 4720 (account created); Security 4698 (task created, needs auditing on); System 7045 (service installed) | Splunk or Event Viewer; MITRE ATT&CK technique pages for context |
| 11 | **Network artifact** (User-Agent, URL pattern, JA3 fingerprint) | Proxy or web logs; packet capture opened in Wireshark | Wireshark filters; ThreatFox (search indicator); ANY.RUN or Hybrid Analysis reports |
| 12 | **C2 or botnet infrastructure** (IP and port, domain) | Firewall or NetFlow logs; Sysmon EID 3; sandbox config extraction | Feodo Tracker; ThreatFox; URLhaus; AbuseIPDB |

## Handling rules
- **Defang** indicators in notes and reports: `hxxps://example[.]com`, `203[.]0[.]113[.]5`.
- **Never click** a link or open an attachment to check it. Use lookups and sandboxes instead.
- **Search before you scan.** On urlscan.io and VirusTotal, look for existing results first. When you must submit, use an Unlisted or private scan so the target is not publicly exposed.
- **Do not upload** real company or personal files to public tools. Search by hash instead.
- **Record the time** of every lookup. Reputation changes, and results from today may differ from the day of the attack.
- **Weigh the source.** A shared IP (Amazon SES, Microsoft 365) with a few spam reports says little about one sender. A look-alike domain or a mismatched Reply-To says more.

## How this shows up in my lab
- **IP:** sample-10's origin IP `5[.]188[.]28[.]177` came from the last `Received` hop and `X-Originating-IP`. Checked in VirusTotal, AbuseIPDB and OTX.
- **Domain:** `linklift[.]space` (sample-10002) was found by decoding a Bing redirect link, then checked in VirusTotal and urlscan.io.
- **Hash:** the PDF in sample-10010 was hashed with a Python script and searched on VirusTotal and OTX without uploading it.
- **Command line:** the Atomic PowerShell test appeared in Sysmon EID 1 as `powershell.exe -e <encoded string>` and was found in Splunk.
- **Account:** the new local account appeared as Security Event 4720 and triggered my "New User Created" alert.
- **Task:** scheduled task creation produced no Event 4698 because auditing was off. That was a logging gap.