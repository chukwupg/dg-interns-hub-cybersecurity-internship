# Q2. Phishing Types and Red-Flag Checklist

## Goal
Compare the main phishing types and list the red flags that give them away.

## Phishing types

| Type | Target | Characteristics | Example red flags |
|---|---|---|---|
| Phishing | Large groups, random users | Mass email, generic wording, fake login or malware link | Generic greeting ("Dear user"), urgent threat, mismatched link, spelling errors |
| Spear phishing | One person or a small group | Researched and personalised; uses name, role, colleagues | Knows your job or manager, unexpected file or link, slightly wrong sender address |
| Whaling | Senior executives (CEO, CFO) | Spear phishing aimed at high-value people; legal, tax or board themes | Urgent "confidential" request, pressure to skip normal approval |
| Smishing | Mobile users via SMS | Short text with a link; delivery, bank or prize themes | Shortened or odd link, unknown number, "act now" pressure |
| Vishing | Phone call victims | Caller poses as bank, IT or police; may spoof caller ID | Asks for OTP, PIN or password; creates panic; asks you to install remote software |
| BEC (Business Email Compromise) | Finance, HR, executives, suppliers | Impersonates or compromises a trusted business account; often no link or attachment | Changed bank details, urgent payment, request to keep it secret, Reply-To differs from From |

## Red-flag checklist
- **Sender:** display name does not match the real address; lookalike domain (letter swaps like rn for m); free email for a business request.
- **Authentication:** SPF, DKIM or DMARC fail or missing (see Q3 and Q4).
- **Urgency or fear:** "account suspended", "pay today", "act within 24 hours".
- **Links:** the visible text differs from the real URL (hover to check); shortened links; odd domains; IP addresses in the URL.
- **Attachments:** unexpected files; macro-enabled Office files; archives; double extensions like `invoice.pdf.exe`.
- **Requests:** asks for credentials, OTP, payment, gift cards or secrecy.
- **Content:** generic greeting, poor grammar, unusual tone for the supposed sender.
- **Context:** you did not expect this message, or it breaks normal process.

## What to do
- Do not click or open. Report it to security or the IT team.
- Check headers and URLs safely (urlscan.io, VirusTotal) without visiting them.
- Verify the request through a second channel you already trust.

## How this shows up in my lab
- I analysed 3 public phishing samples this week (from phishing_pot): sample-10.eml, sample-10002.eml, sample-100010.eml.
- For each, I check the sender, headers, URLs (defanged) and attachment hashes, then give a verdict.
- Verdict: 2 Malicious, 1 Suspicious 
- Red flags I found: 
    - Display name does not match the sender address
    - Failed or missing authentication (SPF none, DKIM fail, no DMARC)
    - Origin is a VPS, not the brand's own mail servers
    - Look-alike extension name using Cyrillic characters
    - Real Google domain used so the link looks trustworthy
    - Fake rating/review notification as the lure