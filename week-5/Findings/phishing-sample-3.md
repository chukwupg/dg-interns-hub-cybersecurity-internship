# Phishing Sample 3: "Payment could be returned" lure with PDF attachment via Amazon SES (sample-10010.eml)

**Week 5 | Hands-on task 1 (Phishing Analysis) | Folder: Findings**

## Goal
Analyse one public phishing sample: read the headers, check URLs without clicking, hash and check the attachment, check reputation, give a verdict and build an IOC table.

## Sample
- **Source:** phishing_pot repository on GitHub, file `sample-10010.eml` (not copied into this repo)
- **Handling:** read as text inside my Kali VM with `triage.py`, which parses headers and URLs and hashes attachments without running them. No links were opened and the PDF was not opened in a reader. The attachment hash was searched on VirusTotal, not uploaded.
- **Recipients anonymised by the dataset** as `phishing@pot`. A second recipient, `admin@wxo[.]HORsXrZA[.]arz`, is also listed. It looks scrambled by the dataset (inference).
- **Lookup timing:** reputation lookups were done on 2026-11-22, about seven months after the email was sent. Results reflect that date, not the send date.

## Basic details

| Field | Value |
|---|---|
| Sender | Get Your YETI Beach Lounge Wagon #87 <Indiamoveasone@procam[.]in> |
| Recipient | To: phishing@pot, admin@wxo[.]HORsXrZA[.]arz. CC: phishing@pot |
| Subject | Your payment could be returned as ... (the subject itself ends in "...") |
| Date | Wed, 01 Apr 2026 22:05:26 +0000 |
| Return-Path | 0101019d4b1479a3-269efb56-d4f9-41b1-9f2d-ff3f851d0d4a-000000@us-west-2[.]amazonses[.]com |
| Reply-To | feedback-ewek16yugnxu4v@listmanage1[.]com (different domain from From) |
| Message-ID | <0101019d4b1479a3-269efb56-d4f9-41b1-9f2d-ff3f851d0d4a-000000@us-west-2[.]amazonses[.]com> |
| X-Originating-IP | not present. `X-SES-Outgoing` shows 54[.]240[.]57[.]30 |
| Content-Type | multipart/mixed (message with attachment) |

![triage output](../Findings/phishing-analysis/phish-s3-01-triage.png)

## Authentication-Results

| Check | Result | Meaning |
|---|---|---|
| SPF | pass (IP 54[.]240[.]57[.]30), smtp.mailfrom us-west-2[.]amazonses[.]com | Passes for Amazon SES's domain, not for procam[.]in, so it is not aligned with the From domain. MXToolbox shows the same: SPF authenticated, SPF alignment failed. |
| DKIM | pass, header.d=procam[.]in and pass, header.d=amazonses[.]com | Message carries a procam[.]in signature and the SES signature. Both share the same body hash. |
| DMARC | pass, action=none, header.from=procam[.]in | Passes through the aligned procam[.]in DKIM signature. The published policy is `p=none`, so nothing is enforced. |
| compauth | pass, reason=100 | Microsoft's combined check. I did not verify what reason code 100 means. |

The DKIM `t=1775081126` timestamp converts to 2026-04-01 22:05:26 UTC, which matches the Date header.

**Observation:** MXToolbox showed an empty public key for the procam[.]in DKIM selector and marked "DKIM Authenticated" as a problem. Microsoft's own result says the signature was verified. My inference is that this is a lookup limitation, not a real failure. I used the receiving server's result.

**My interpretation (inference, not proven):** the message was sent through Amazon SES using a DKIM key for procam[.]in. Either the procam[.]in owner sent it, or its SES account or keys were compromised or abused. The headers cannot tell me which. Passing authentication shows the message is genuine SES mail for procam[.]in. It does not show the content is safe.

## Received chain (read bottom to top, numbered as MXToolbox does)

| Hop | Time (UTC) | Detail |
|---|---|---|
| 1 (origin) | 22:05:27 | `a57-30.smtp-out.us-west-2.amazonses[.]com` (54[.]240[.]57[.]30) to `BL6PEPF00020E5F.mail.protection.outlook[.]com` (10[.]167[.]249[.]20), TLS1.3. MXToolbox flags this hop as on a blacklist. |
| 2 | 22:05:27 | `BL6PEPF00020E5F` to `MN2PR03CA0019.outlook.office365[.]com`, TLS1.3 |
| 3 | 22:05:28 | `MN2PR03CA0019` to `PH0PR10MB5609`, TLS1.2 |
| 4 | 22:05:30 | `PH0PR10MB5609` to `MW4PR10MB5749`, HTTPS (mailbox delivery) |

Total delay was 3 seconds. The first hop is Amazon SES and every later hop is Microsoft, so there is no other originating IP. 54[.]240[.]57[.]30 is a shared Amazon SES IP, so its reputation says little about this sender. The blacklist flag does not name the list. It is consistent with the spam reports on AbuseIPDB.

## URL analysis (not clicked)

| URL | Notes |
|---|---|
| hxxp://23nbpth9[.]r[.]us-west-2[.]awstrack[.]me/L0/%2F/1/0101019d...-000000/... | SES click-tracking link over plain HTTP. The wrapped target URL-decodes to `/`, which I did not verify further. |
| hxxps://23nbpth9[.]r[.]us-west-2[.]awstrack[.]me/I0/0101019d...-000000/... | SES tracking link, probably an open-tracking pixel (inference) |
| hxxps://23nbpth9[.]r[.]us-west-2[.]awstrack[.]me/L0/hxxps:%2F%2Flistmanage1[.]com%2F431_1_9968lip7LCQtV8bMda0[.]x6fwC2976454_4M0UY7z2q_6[.]2/1/... | Click-tracking link wrapping `hxxps://listmanage1[.]com/431_1_9968lip7LCQtV8bMda0[.]x6fwC2976454_4M0UY7z2q_6[.]2` |
| hxxp://www[.]njm[.]com/ | VirusTotal 0/92. I did not see where it appears in the email, so I treat it as context only. |

- awstrack[.]me is Amazon's tracking domain, so its reputation says little. The IOC to track is `listmanage1[.]com`, which is both the Reply-To domain and the tracked-link destination.
- `triage.py` did not print the body text or link text, so I did not review what the visible links say.

## Attachment

| Field | Value |
|---|---|
| Filename | phishing@pot.pdf (probably the dataset's anonymisation of the original name, inference) |
| Type | application/pdf |
| Size | 18354 bytes |
| SHA256 | 3351250345e4b65b906dd100aef7aafed2b4560c59f881d5112cb24acc661735 |

| Tool | Result |
|---|---|
| VirusTotal (hash search) | 1/60 vendors flagged it. **Code Insight** describes the file as non-functional and severely malformed (no Catalog object, no Info dictionary, no rendered pages or text). It reports no embedded JavaScript, launch actions or URLs, and classifies it as benign, likely a corrupted fragment. |
| AlienVault OTX (hash) | 0 pulses, 0 AV detections, 0 IDS detections, 0 YARA detections, 0 alerts |

The PDF is not a working delivery vehicle for malware or a link, so the attachment is not the main evidence in this sample. I do not know why it is malformed. It may have been corrupted or altered when the dataset was built (inference). I relied on VirusTotal's analysis and did not run local PDF tools.

![VirusTotal hash](../Findings/phishing-analysis/phish-s3-02-virustotal-codeinsight.png)


## Reputation checks

| Indicator | Tool | Result |
|---|---|---|
| 54[.]240[.]57[.]30 (Amazon SES, AS16509, Boardman OR) | VirusTotal | 0/92, all vendors unrated |
| | AbuseIPDB | 4% confidence ("Caution"), 37 reports from 8 reporters, latest 4 days before lookup. Nearly all recent reports are from one reporter (xmission[.]com) and tagged Email Spam. |
| | AlienVault OTX | Verdict "Whitelisted", 0 pulses, 0 passive DNS. Reverse DNS `a57-30.smtp-out.us-west-2.amazonses[.]com` |
| procam[.]in | VirusTotal | 0/92 |
| | Whois | Created 2007-05-04 (about 19 years old). Registrar GoDaddy. Registrant organisation Procam International Pvt Ltd, Maharashtra, IN. Updated 2026-04-29. |
| | AlienVault OTX | 0 pulses, 356 passive DNS records, 20 URLs, 21 subdomains, main IP 75[.]2[.]60[.]5 (AWS), SPF record present. Subdomains include `tatamumbaimarathon[.]procam[.]in`. The OTX WHOIS expiry (2023) is stale. |
| | urlscan.io | One manual scan (2026-11-22). No classification. Page title "Welcome to Procam International", 45 requests, Google Analytics and Tag Manager only. |
| | DMARC / SPF (MXToolbox) | DMARC record `v=DMARC1; p=none;`, valid syntax, no enforcement. SPF checked against the SES domain: `v=spf1 include:amazonses.com -all` |
| listmanage1[.]com | VirusTotal | 0/92 |
| | Whois | "No match for domain": **not registered at lookup time** |
| | AlienVault OTX | 0 pulses, 40 passive DNS records, 9 URLs, 2 subdomains. Domain not currently resolving. Passive DNS shows Cloudflare IPs from 2026-01-11 to 2026-02-23. URL checks in Aug 2026 gave connection errors. |
| | urlscan.io | No result. DNS error: the domain could not be resolved, so urlscan did not load it. |
| njm[.]com | VirusTotal | 0/92 |
| Full headers | MXToolbox | 4 hops, 3 s delay. DMARC record found with `p=none`. SPF alignment failed and DKIM alignment passed. Hop 1 (54[.]240[.]57[.]30) flagged as on a blacklist. |

![VirusTotal](../Findings/phishing-analysis/phish-s3-02-virustotal-1.png)
![VirusTotal](../Findings/phishing-analysis/phish-s3-02-virustotal-2.png)
![AbuseIPDB](../Findings/phishing-analysis/phish-s3-03-abuseipdb.png)
![AlienVault OTX](../Findings/phishing-analysis/phish-s3-04-otx-1.png)
![AlienVault OTX](../Findings/phishing-analysis/phish-s3-04-otx-2.png)
![AlienVault OTX](../Findings/phishing-analysis/phish-s3-04-otx-3.png)
![AlienVault OTX](../Findings/phishing-analysis/phish-s3-04-otx-4.png)
![urlscan.io](../Findings/phishing-analysis/phish-s3-05-urlscan-1.png)
![urlscan.io listmanage1 DNS error](../Findings/phishing-analysis/phish-s3-05-urlscan-2.png)
![MXToolbox](../Findings/phishing-analysis/phish-s3-06-mxtoolbox-1.png)
![MXToolbox](../Findings/phishing-analysis/phish-s3-06-mxtoolbox-2.png)
![Whois](../Findings/phishing-analysis/phish-s3-07-whois-1.png)
![Whois](../Findings/phishing-analysis/phish-s3-07-whois-2.png)

**Useful findings from the reputation checks:**
- **Reply-To / link domain is gone.** `listmanage1[.]com` is not registered now, and passive DNS last saw it resolving in February 2026. Its subdomain names (`us12.`, `unhcr-us6.`) look like per-customer tracking subdomains of a bulk-mail service, and the name resembles Mailchimp's `list-manage.com` (inference, not confirmed). I cannot say whether it resolved on 2026-04-01, and replies to the Reply-To address would not be deliverable now. An unregistered look-alike can be registered by anyone, so it should be blocked.
- **Sender domain is legitimate.** `procam[.]in` belongs to an established company (Procam International, which runs marathon events judging by its subdomains) and has been registered since 2007. A "YETI Beach Lounge Wagon" giveaway and a payment warning have no visible link to that business. This points to abuse of the company's SES sending, or a compromised account (inference).
- **Shared sending IP.** 54[.]240[.]57[.]30 has a low abuse score driven by spam reports from one reporter. This is background noise about a shared Amazon SES IP, not evidence about this sender.

## Related indicators (seen in OTX, not present in the email)

| Type | Value | Context |
|---|---|---|
| Domain | us12[.]listmanage1[.]com | Subdomain in passive DNS (Jan to Feb 2026) |
| Domain | unhcr-us6[.]listmanage1[.]com | Subdomain in passive DNS (Jan 2026) |
| IP | 104[.]21[.]65[.]191, 172[.]67[.]165[.]123 | Cloudflare IPs the listmanage1[.]com subdomains resolved to. Shared by many sites, so low value. |

These are context for hunting, not confirmed parts of this email.

## IOC table (defanged)

| Type | Value | Context | Reputation |
|---|---|---|---|
| Email | Indiamoveasone@procam[.]in | Sender (From) | n/a |
| Display name | Get Your YETI Beach Lounge Wagon #87 | Lure brand / giveaway theme | n/a |
| Email | feedback-ewek16yugnxu4v@listmanage1[.]com | Reply-To | n/a |
| Domain | procam[.]in | Sender and DKIM d= | VT 0/92; created 2007; urlscan no classification |
| Domain | listmanage1[.]com | Reply-To domain and tracked-link destination | VT 0/92; not registered at lookup; OTX 40 passive DNS records, not resolving |
| IP | 54[.]240[.]57[.]30 | Amazon SES sending IP | VT 0/92; AbuseIPDB 4%; OTX whitelisted |
| Domain | 23nbpth9[.]r[.]us-west-2[.]awstrack[.]me | SES click-tracking host in the email | Not checked (Amazon tracking domain) |
| URL | hxxps://listmanage1[.]com/431_1_9968lip7LCQtV8bMda0[.]x6fwC2976454_4M0UY7z2q_6[.]2 | Decoded link destination | Not checked; domain unregistered |
| URL | hxxps://23nbpth9[.]r[.]us-west-2[.]awstrack[.]me/L0/hxxps:%2F%2Flistmanage1[.]com%2F... | Tracked lure link (full URL in sample) | Not checked |
| Domain | njm[.]com | Linked in the email, context only | VT 0/92 |
| File hash (SHA256) | 3351250345e4b65b906dd100aef7aafed2b4560c59f881d5112cb24acc661735 | phishing@pot.pdf, 18354 bytes, malformed PDF | VT 1/60; OTX 0 detections |
| Message-ID | 0101019d4b1479a3-269efb56-d4f9-41b1-9f2d-ff3f851d0d4a-000000@us-west-2[.]amazonses[.]com | Message identifier (SES ID) | n/a |

## Verdict
**Suspicious (likely spam or a phishing attempt), moderate confidence.**

Justification:
- The display name is a brand giveaway ("YETI Beach Lounge Wagon") but the subject is a payment warning, so the two do not match, and neither relates to the sending company's apparent business.
- The Reply-To and the tracked link point to `listmanage1[.]com`, a different domain from the sender. It looks like a look-alike of a bulk-mail tracking domain and is not registered now (the look-alike point is inference).
- The message carries an unrelated attachment, and the To field mixes the anonymised address with a random-looking one.
- SPF, DKIM, DMARC and compauth all pass, so the message is genuine Amazon SES mail signed for `procam[.]in`. This points to abuse of a legitimate sending account or service (inference), and the verdict rests on content and infrastructure, not on authentication.
- I am not rating it **Malicious** because the PDF is malformed with no payload or URLs, every reputation lookup is clean, the sender domain is old and legitimate, and I did not see what the body asks the recipient to do.
- **Limitation:** if the body asks for payment or credentials, or the tracked link led to a credential page, this would move to Malicious.

## Red flags identified
- Display name and subject mismatch (giveaway brand versus payment warning)
- Display name and subject unrelated to the sending company
- Reply-To domain differs from the From domain
- Reply-To and link domain is a look-alike of a bulk-mail tracking domain, now unregistered
- Attachment in an unsolicited message (malformed PDF)
- Links hidden behind SES click-tracking redirects, one over plain HTTP
- Random-looking second recipient on an odd domain
- Authentication passes even though the content is suspicious (abuse of a legitimate sending service)
- Sending IP is on a blacklist per MXToolbox (shared SES IP)

## Recommendations
- Block the sender address, the Reply-To address and `listmanage1[.]com` and its subdomains at the mail gateway.
- Block the attachment by SHA256 and search mail logs for the same hash.
- Alert on mail whose DKIM d= is `procam[.]in` and whose Reply-To domain differs.
- Report the message to Amazon SES abuse and to the owner of `procam[.]in` as a possible compromised sending account.
- Warn users that "payment returned" messages with a PDF are a common lure.

## Limitations
- I did not view the email body or any landing page, so I cannot say what the message asks the recipient to do.
- I did not run local static analysis on the PDF. I relied on VirusTotal's analysis.
- I did not look up `awstrack[.]me` or the decoded `listmanage1[.]com` URL on VirusTotal.
- I did not verify what compauth reason 100 means.
- The resemblance of `listmanage1[.]com` to Mailchimp's tracking domain is inferred from naming patterns only.

## What I learned
- SPF, DKIM, DMARC and compauth can all pass for a suspicious message sent through a legitimate bulk-mail service, so authentication results do not show that the content is safe.
- Shared sending IPs make IP reputation weak. The Amazon SES IP had a low abuse score from spam reports that say little about this sender.
- Clean reputation across tools does not make a message benign. The useful evidence here was the Reply-To and link domain mismatch, the look-alike domain that is no longer registered, and the subject and display name mismatch.
- A hash search and VirusTotal's Code Insight let me assess an attachment without opening it. In this case it showed the PDF was malformed and carried no payload.