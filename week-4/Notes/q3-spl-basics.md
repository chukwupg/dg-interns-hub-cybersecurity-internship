# Q3: SPL basics — search, where, stats, table, eval, timechart, rex

| Command | What it does | Example |
|---|---|---|
| `search` (implicit) | Filters events by keyword/field match | `index=lab sourcetype="WinEventLog:Security" EventCode=4625` |
| `where` | Filters results after a calculation/comparison, works on fields `stats`/`eval` produce | `... | stats count by src_ip | where count >= 5` |
| `stats` | Aggregates events into summary statistics (count, sum, avg, etc.) grouped by field(s) | `... | stats count by Account_Name` |
| `table` | Displays only the chosen fields in a table, in the order given | `... | table _time, host, Image, CommandLine` |
| `eval` | Creates/modifies a field using an expression | `... | eval risk=if(count>10,"high","low")` |
| `timechart` | Aggregates events over time buckets, good for trend charts | `... | timechart span=1h count by sourcetype` |
| `rex` | Extracts a field from raw text using a regex | `... | rex field=_raw "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"` |

## How this shows up in my lab
- My SSH brute-force detection used `rex` to pull `src_ip` out of `auth.log`'s raw text, then `stats count by src_ip` and `where count >= 5` to flag repeat offenders — this is exactly the brief's recommended brute-force logic.
- I used `table` to format the PowerShell and new-user-creation searches into readable columns for screenshots.