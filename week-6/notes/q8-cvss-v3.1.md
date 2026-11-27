# Q8: CVSS v3.1

## Base metrics
- **Attack Vector (AV):** How the vulnerability is reached - Network, Adjacent, Local, Physical.
- **Attack Complexity (AC):** How hard it is to exploit once conditions are met - Low or High.
- **Privileges Required (PR):** What access level the attacker needs beforehand - None, Low, High.
- **User Interaction (UI):** Whether a victim must do something (e.g. click a link) - None or Required.
- **Scope (S):** Whether the exploited component's impact extends beyond itself to another component - Unchanged or Changed.
- **Confidentiality / Integrity / Availability (C/I/A):** The degree of impact on each - None, Low, High.

## Severity bands
| Score | Severity |
|---|---|
| 0.0 | None |
| 0.1-3.9 | Low |
| 4.0-6.9 | Medium |
| 7.0-8.9 | High |
| 9.0-10.0 | Critical |

## Worked findings from this week

**1. SQL Injection:** `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` - **8.8 (High)**
Reachable over the network, low complexity, requires a logged-in user (PR:L), no user interaction, and I demonstrated full read access to database contents (C:H), with the potential for write/availability impact given typical DB privileges (I:H, A:H).

**2. Reflected XSS:** `AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N` - **6.1 (Medium)**
Requires a victim to click a crafted link (UI:R), and the impact extends to the victim's browser session beyond the vulnerable component (S:C), but confidentiality/integrity impact is limited to what a stolen session enables (C:L/I:L).

**3. Brute Force:** `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` - **9.1 (Critical)**
No authentication needed to attempt it, no user interaction, and a successful attack gives full account takeover (C:H/I:H). I judged this High/Critical because I demonstrated actually recovering a working credential, not just that the form lacked a lockout.

## How this shows up in my lab
I used these exact CVSS scores in my Findings files and VAPT report this week, scored from what I actually demonstrated rather than worst-case theory.