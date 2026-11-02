# Q8. What is a baseline, and why does it matter?

## Definition
- A baseline is a record of what "normal" looks like on your network and systems over time.

## What it can cover
| Area | Examples |
|---|---|
| Network | Usual protocols, top talkers, volumes, busy hours, normal DNS queries |
| Hosts | Usual processes, services, startup items, installed software |
| Accounts | Normal logon times, locations and logon types, usual admin activity |

## Why a SOC analyst needs it
- Alerts only make sense against normal: a thousand DNS queries may be routine on one network and an attack on another.
- It speeds up triage: you spot the odd event instead of reading everything.
- It reduces false positives when rules are tuned to what is normal.
- It shows change over time, such as a new service or a new admin.

## How to build one
- Capture traffic and log samples during normal use, note the usual patterns, and review them regularly.

## How this shows up in my lab
- Type 5 logons and my normal Apache traffic are examples of normal on my VMs.

- Because I know the usual events, the failed logons, the new `labtest` account and the SYN burst stand out.
