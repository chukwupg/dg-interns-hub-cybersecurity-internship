# Q3. SPF, DKIM and DMARC

## Goal
Explain what each email authentication method checks, with a pass and a fail example.

## Overview

| Method | What it checks | Where the result comes from | How it can fail |
|---|---|---|---|
| **SPF** (Sender Policy Framework) | Is the sending server's IP allowed to send for the envelope sender domain (the `MAIL FROM` / Return-Path domain)? | A DNS TXT record on the domain listing allowed IPs and servers | Sender IP not in the record; no record; too many lookups |
| **DKIM** (DomainKeys Identified Mail) | Was the message signed by the domain, and was it changed in transit? | A digital signature in the `DKIM-Signature` header; public key in DNS | Signature does not verify, key missing, message altered |
| **DMARC** | Does SPF or DKIM pass **and align** with the domain in the visible `From:` header? What should receivers do if not? | A DNS TXT record at `_dmarc.<domain>` with a policy | Neither SPF nor DKIM passes with alignment |

## Key ideas
- SPF checks the **envelope** sender, not the `From:` address the user sees. That gap is why DMARC exists.
- DKIM proves a domain signed the message, not that the message is safe.
- **Alignment:** the domain that passed SPF or DKIM must match the `From:` domain.
- DMARC policies: `none` (monitor only), `quarantine` (treat as suspicious, often spam folder), `reject` (block).
- A pass is not proof the email is safe. An attacker can send from their own lookalike domain with valid SPF, DKIM and DMARC.

## Example 1: pass (illustrative, made-up values)
```
Authentication-Results: mx.example.net;
 spf=pass (sender IP is 203.0.113.25) smtp.mailfrom=example.com;
 dkim=pass header.d=example.com header.s=selector1;
 dmarc=pass (p=REJECT) header.from=example.com
```
- SPF passed: the sending IP is allowed for example.com.
- DKIM passed: valid signature from example.com.
- DMARC passed: results align with the From domain.

## Example 2: fail (illustrative, made-up values)
```
Authentication-Results: mx.example.net;
 spf=fail (sender IP is 198.51.100.77) smtp.mailfrom=example.com;
 dkim=fail (body hash did not verify) header.d=example.com;
 dmarc=fail (p=REJECT) header.from=example.com
```
- SPF failed: the IP is not allowed to send for example.com.
- DKIM failed: the message was altered or the signature is not valid.
- DMARC failed: with `p=reject` this message should be blocked. Likely spoofing.

## How this shows up in my lab
- Real headers from my phishing samples: [[paste the Authentication-Results line for each sample]]
- Results I saw: SPF [[pass/fail/none]], DKIM [[...]], DMARC [[...]] for sample [[name]]
- I can cross-check with the MXToolbox email header analyzer: [[screenshot link]]
- My own lab has no mail server, so I only analyse public samples.