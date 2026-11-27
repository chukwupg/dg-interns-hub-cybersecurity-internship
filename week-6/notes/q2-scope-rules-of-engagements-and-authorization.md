# Q2: Scope, Rules of Engagement and Authorization

## Why they come first
- **Legal protection:** Testing a system without authorization is illegal in most jurisdictions, regardless of intent.
- **Prevents collateral damage:** Clear scope stops testers from accidentally hitting production systems or third parties.
- **Sets expectations:** Both sides agree on timing, methods and what counts as acceptable risk (e.g. is DoS testing allowed?).
- **Defines success:** Without agreed objectives, a test can wander and miss what the client actually cares about.

## Rules of Engagement (RoE) template

| Field | Description |
|---|---|
| 1. Authorized parties | Who is performing the test and who signed it off on the client side |
| 2. Scope (in-scope assets) | Exact IPs, domains, applications included |
| 3. Out-of-scope assets | Systems explicitly excluded |
| 4. Testing window | Start/end dates and permitted hours |
| 5. Testing types permitted | e.g. manual, automated scanning, social engineering, DoS allowed or not |
| 6. Emergency contact | Who to call if something breaks |
| 7. Data handling rules | How findings/evidence are stored and who can see them |
| 8. Communication plan | How often status updates are sent, and through what channel |
| 9. Legal sign-off | Signature/date of written authorization |
| 10. Rollback expectations | What testers must restore if something changes (accounts, data) |

## How this shows up in my lab
Since DVWA and Metasploitable 2 are my own VMs on an isolated host-only network (192.168.98.0/24), I am both the authorizing party and the tester. I still apply the same discipline: scope is limited to these two VMs, never the host OS or anything outside 192.168.98.0/24, and I never bridge these VMs to the internet.