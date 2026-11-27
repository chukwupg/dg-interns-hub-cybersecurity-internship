# Q3: OWASP Top 10

Note: OWASP released a Top 10:2025 update. This week's labs (DVWA) map to the 2021 categories, so I've used that list below, as the brief specifies.

| Category | Example | Impact | Fix |
|---|---|---|---|
| A01: Broken Access Control | A user edits a URL parameter to view another user's data | Unauthorized data access/modification | Enforce access control server-side on every request |
| A02: Cryptographic Failures | Passwords stored in plain text or weak hashing | Credential theft if DB is breached | Use strong hashing (bcrypt/Argon2), encrypt data in transit (TLS) |
| A03: Injection | SQL injection, as demonstrated in DVWA this week | Data theft, modification, or full DB compromise | Parameterized queries / prepared statements |
| A04: Insecure Design | No rate limiting on login, by design | Brute force becomes trivial | Threat model the feature before building it |
| A05: Security Misconfiguration | Default credentials left on a server | Easy unauthorized access | Harden configs, disable defaults, remove unused features |
| A06: Vulnerable and Outdated Components | Running an old, unpatched library with known CVEs | Exploitation via known public exploits | Patch management, dependency scanning |
| A07: Identification and Authentication Failures | Weak session IDs, no account lockout (DVWA brute force module) | Account takeover | MFA, strong session management, lockout policies |
| A08: Software and Data Integrity Failures | Installing unsigned/unverified updates or plugins | Supply chain compromise | Verify signatures, use trusted sources/CI pipelines |
| A09: Security Logging and Monitoring Failures | No logs when an attacker brute-forces a login | Attacks go undetected for long periods | Centralized logging, alerting on suspicious patterns |
| A10: Server-Side Request Forgery (SSRF) | App fetches a URL supplied by the user with no validation | Attacker can reach internal-only services | Validate/allowlist outbound destinations |

## How this shows up in my lab
This week I directly demonstrated A03 (SQL injection, XSS, command injection) and A07 (brute force) in DVWA. ZAP's passive scan also flagged A05-type issues (missing security headers, CSP problems) without any manual exploitation needed.