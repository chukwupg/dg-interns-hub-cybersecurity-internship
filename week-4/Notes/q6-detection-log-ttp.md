# Q6: Detection logic from a TTP — SSH/Windows brute force, mapped to T1110

## Detection logic
**Trigger**: 5 or more failed logon attempts from the same source within a 5-minute window, targeting the same or multiple accounts on one host.

**SSH (Linux) version** — built and tested in my lab:
```spl
index=lab source="/var/log/auth.log" "Failed password"
| rex field=_raw "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| bucket _time span=5m
| stats count by _time, src_ip, host
| where count >= 5
```

**Windows version** (EventCode 4625), using the same logic:
```spl
index=lab sourcetype="WinEventLog:Security" EventCode=4625
| bucket _time span=5m
| stats count by _time, Account_Name, Source_Network_Address
| where count >= 5
```

## MITRE mapping
- **T1110 – Brute Force**: repeated logon attempts to guess credentials. Both searches above detect this technique, just on different log sources (SSH auth vs Windows Security log).

## How this shows up in my lab
- My Hydra run against Ubuntu (192.168.98.129) from Kali (192.168.98.130) generated ~20 failed attempts in a few seconds — well over the 5-in-5-minutes threshold, confirmed by my "SSH Bruteforce" scheduled alert built from search #4.
- I did not run a matching Windows brute-force attack this week (that would need something like a Hydra RDP/SMB module or a scripted login loop), so the Windows version above is documented logic, not a tested result.