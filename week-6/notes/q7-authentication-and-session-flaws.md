# Q7: Authentication and Session Flaws

| Flaw | Description | How a SOC analyst would detect it |
|---|---|---|
| Brute force | Repeated login attempts guessing credentials, with no lockout | High volume of failed login events from one source IP/account in a short window (auth logs, SIEM alert) |
| Weak session IDs | Session tokens are predictable or too short, allowing guessing/hijacking | Monitoring for session ID reuse across different IPs/user-agents, or anomaly detection on session token entropy |
| Missing cookie flags | Session cookies lack `HttpOnly` (readable by JS, so stealable via XSS), `Secure` (sent over plain HTTP), or `SameSite` (sent on cross-site requests, enabling CSRF) | Passive scanning (ZAP flags these automatically) or manual inspection of Set-Cookie headers |

## How this shows up in my lab
I confirmed brute force directly: Hydra recovered a valid DVWA admin password using rockyou.txt with no lockout or rate limiting. ZAP's passive scan also flagged DVWA's login cookies for missing `HttpOnly` and `SameSite` attributes. A SOC analyst watching this lab's traffic would see a spike of failed-login HTTP responses from a single Kali IP in a short window, a classic brute-force signature.