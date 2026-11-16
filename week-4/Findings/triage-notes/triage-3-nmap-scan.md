# Triage Note 3: Nmap SYN scan (manual search, no alert configured)

- **Who:** No specific account, this is network-level recon, not an authentication event.
- **What:** An Nmap `-sS` (SYN/half-open) scan was run from Kali against the Ubuntu VM. I checked `auth.log` in Splunk afterward and found no corresponding entries.
- **When:** 11/15/26 - 01:47:32 AM
- **Where:** Source 192.168.98.130 (Kali) - destination 192.168.98.129 (Ubuntu), all/common TCP ports.
- **Why / Verdict:** **True positive for "activity occurred," but a detection gap** - the scan genuinely happened (I ran it), but it produced **no log entry** in the sources I'm ingesting, because a half-open SYN scan never completes the SSH application handshake that `auth.log` records. This is a real finding, not a failure: my current SIEM setup has no visibility into network-level recon unless I ingest packet-capture or firewall/IDS data (e.g. Snort, which I'm not feeding into Splunk this week).
- **Next step:** To close this gap, I would ingest Snort or firewall logs into Splunk, or add a host-based control (e.g. `fail2ban`-style connection-rate logging) that *does* record incoming SYN activity.