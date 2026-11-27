# Q5: XSS and CSRF

## XSS types

| Attack Type | How It Works | Mitigation |
|---|---|---|
| Reflected XSS | Malicious script in a request (e.g. URL parameter) is immediately reflected back in the response and executes | Output encoding for the HTML context, input validation, CSP |
| Stored XSS | Malicious script is saved server-side (e.g. in a comment/message) and executes for every visitor who views it later | Output encoding at render time, sanitize input at submission, CSP |
| DOM-based XSS | The vulnerability is in client-side JavaScript that writes untrusted data into the DOM, without the payload ever reaching the server | Avoid unsafe sinks (`innerHTML`, `eval`), use safe DOM APIs, CSP |
| CSRF | A malicious site tricks a logged-in user's browser into submitting a request to a trusted site using their active session | Anti-CSRF tokens, SameSite cookies, re-authentication for sensitive actions |

## Mitigation detail
- **Output encoding:** Convert special characters (`<`, `>`, `"`, `'`) to their HTML entity equivalents so browsers render them as text, not executable markup.
- **CSP (Content-Security-Policy):** An HTTP header that restricts which script sources a page can execute, reducing XSS impact even if a payload slips through.
- **Anti-CSRF tokens:** A unique, unpredictable token included in each form/request that the server validates, so a forged cross-site request (which can't know the token) is rejected.

## How this shows up in my lab
I confirmed reflected XSS (dialog fired on submission) and stored XSS (payload persisted and fired on every reload) in DVWA at Low. At Medium, the plain `<script>` tag was blocked, but `<img src=x onerror="alert(...)">` bypassed the filter; showing the filter blocks a keyword, not the underlying risk. ZAP's passive scan also flagged the app for missing a CSP header and missing anti-CSRF tokens.