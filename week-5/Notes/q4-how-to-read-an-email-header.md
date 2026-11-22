# Q4. How to Read an Email Header

## Goal
Explain the main header fields and what suspicious values look like.

## How to read it
- Open "Show original" or "View source" to see the full raw header.
- **Received** lines are added by each mail server. Read them **from bottom to top**: the bottom one is closest to the sender, the top one is the last hop to you.
- Only trust Received lines added by servers you trust. Attackers can add fake ones at the bottom.

## Header fields

| Header field | Purpose | Red flag indicator |
|---|---|---|
| **From** | Sender shown to the user | Display name does not match address; lookalike or free-mail domain |
| **To / Cc / Bcc** | Recipients | Many unrelated recipients; you are in Bcc; your address is missing |
| **Subject / Date** | Topic and time sent | Urgent wording; date or time zone odd for the sender |
| **Received** (chain) | Path through mail servers, with IPs and timestamps | Unexpected country or host; big time jumps; mismatched hostname and IP; broken chain |
| **Return-Path** | Envelope sender; where bounces go; used by SPF | Differs from From domain; random or unrelated domain |
| **Reply-To** | Where replies go | Different from From (common in BEC); free-mail address |
| **Message-ID** | Unique ID created by the sending system | Domain does not match sender domain; missing; odd format |
| **Authentication-Results** | Receiver's SPF, DKIM and DMARC verdicts | Any fail, `none`, `softfail`, or missing |
| **X-Originating-IP / X-Mailer** (if present) | Client IP or software used | IP from unexpected location; bulk-mail tool for a "personal" email |
| **Content-Type / attachments** | Message structure | Executable or macro attachment; HTML-only body hiding links |

## Quick workflow
1. Read From, Return-Path and Reply-To and compare the domains.
2. Read Authentication-Results.
3. Trace the Received chain bottom to top and note the origin IP.
4. Check the origin IP and domains in AbuseIPDB, VirusTotal and AlienVault OTX.
5. Check Message-ID and any URLs (defanged) and attachment hashes.
6. Give a verdict: benign, suspicious or malicious, with reasons.

## How this shows up in my lab
- I read the headers of 3 phishing samples and compare the fields above
- I check origin IPs and domains with AbuseIPDB, OTX and VirusTotal
- Tools: MXToolbox header analyzer and CyberChef, (to decode encoded text) in addition to a python email header parser [emails-and-triage-script](../Findings/phishing-analysis/emails-and-traige-script/)