# Q9: Tool Comparison

| Tool | Purpose | Manual or Automated | Free or Paid |
|---|---|---|---|
| Burp Suite (Community) | Intercepting proxy, manual request manipulation, some automated scanning (paid tiers) | Mostly manual (Community); automated scanner is Pro-only | Free (Community) / Paid (Pro) |
| OWASP ZAP | Automated spider + active/passive scanning, intercepting proxy | Both | Free |
| Nmap | Network/port scanning and service/version detection | Automated | Free |
| Nikto | Web server scanner for known misconfigurations and outdated software | Automated | Free |
| sqlmap | Automated SQL injection detection and exploitation | Automated | Free |
| Hydra | Automated credential brute-forcing against login forms/services | Automated | Free |

## How this shows up in my lab
I used Nmap for recon on both targets, ZAP for the automated DVWA scan, and Hydra for the brute-force finding this week. I didn't use Burp, Nikto or sqlmap this week since the brief's tool list for this task is for the comparison table, not required for every lab task but I used Firefox DevTools as a lightweight alternative to Burp for capturing requests.