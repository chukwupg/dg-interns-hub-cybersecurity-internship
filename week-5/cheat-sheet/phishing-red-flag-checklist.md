# Phishing Red-Flag Checklist

**Week 5 | Cheat Sheet | Folder: Cheat Sheet**

Work through each section for every suspicious email. Tick what you find, and read the result at the bottom. Do not click links or open attachments while checking.

## 1. Sender
- [ ] Display name does not match the email address
- [ ] Domain is a look-alike (swapped letters, extra words, odd characters, unrelated company)
- [ ] Free or personal email address used for a business or brand message
- [ ] Return-Path or Reply-To domain differs from the From domain
- [ ] Sender address looks random or auto-generated

## 2. Headers and authentication
- [ ] SPF, DKIM or DMARC shows fail, none or softfail
- [ ] Signing domain (`d=`) is unrelated to the From domain
- [ ] First `Received` hop is a hosting provider or country that does not fit the sender
- [ ] Message-ID domain does not match the sender
- [ ] Authentication passes but the content is still suspicious (abused legitimate service)

## 3. Subject and body
- [ ] Urgency or fear: account suspended, payment returned, act within 24 hours
- [ ] Generic greeting ("Dear user") or wrong name
- [ ] Unexpected prize, refund, invoice, delivery notice or government notice
- [ ] Poor grammar or an unusual tone for the supposed sender
- [ ] Subject theme and body or link destination do not match

## 4. Links
- [ ] Visible text differs from the real address (hover to check)
- [ ] Link goes through a redirect or tracking domain that hides the destination
- [ ] Shortened link, IP address in the URL, or a plain `http://` link
- [ ] Look-alike characters or names (for example Cyrillic letters in a brand name)
- [ ] Real service domain used for a fake page (store listing, shared document, form)

## 5. Attachments
- [ ] Attachment not expected
- [ ] Macro-enabled Office file, HTML file, archive, or a double extension like `invoice.pdf.exe`
- [ ] Password-protected archive with the password in the email
- [ ] Hash is flagged on VirusTotal (search by hash only)

## 6. Requests
- [ ] Asks for a password, one-time code, card number or personal details
- [ ] Asks for payment, gift cards, or a change of bank details
- [ ] Asks you to install software or an extension, or to enable macros
- [ ] Asks you to keep the request secret or skip normal approval

## 7. Context
- [ ] You did not expect this message or have no relationship with the sender
- [ ] The request breaks your normal process
- [ ] A second trusted channel (phone call, known number) does not confirm it

## What the result means

| Result | Verdict | Action |
|---|---|---|
| A request for credentials, payment or software **plus** any mismatched sender, link or failed authentication | **Malicious** | Report, block, do not interact |
| Several flags from sections 1 to 4 but no clear request | **Suspicious** | Report, check indicators, escalate if unsure |
| One minor flag, everything else checks out | **Likely benign** | Verify with the sender through another channel |

Clean results on reputation tools do **not** clear an email. Judge the content, headers and links first.

## Safe checks (all free)
- **Headers:** MXToolbox Email Header Analyzer or manual reading
- **Links:** urlscan.io (search first, Unlisted scan), VirusTotal, URLhaus
- **Domains and IPs:** VirusTotal, AlienVault OTX, AbuseIPDB, whois
- **Attachments:** hash with `sha256sum` or `Get-FileHash`, then search VirusTotal
- **Encoded text:** CyberChef

## If it is phishing
1. Do not click, reply or forward it to colleagues.
2. Keep the original `.eml` file as evidence.
3. Report it to the security team or mail provider.
4. Block the sender, domains and hashes, and search mailboxes for the same indicators.
5. If anyone clicked or entered details, reset the password and check the account for new rules or logins.