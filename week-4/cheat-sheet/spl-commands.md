<!-- cheatsheet-spl-commands.md -->
# Cheat Sheet: SPL Commands

| Command | What it does | When to use |
|---|---|---|
| `search` (implicit) | Filters events by keyword or field=value match | Starting point of almost every query, e.g. `index=lab sourcetype="WinEventLog:Security"` |
| `where` | Filters results after a stats/eval calculation | Narrowing aggregated results, e.g. `... \| where count >= 5` |
| `stats` | Aggregates events into summary stats grouped by field(s) | Counting events per user/IP/host |
| `table` | Shows only chosen fields, in the given order | Making a readable results table for a report/screenshot |
| `eval` | Creates or modifies a field using an expression | Tagging results, e.g. `eval risk=if(count>10,"high","low")` |
| `timechart` | Aggregates events into time buckets for trending | Spotting spikes over time, e.g. login failures per hour |
| `rex` | Extracts a field from raw text with a regex | Pulling an IP or username out of unstructured log text |
| `bucket` | Rounds `_time` (or another field) into discrete bins | Grouping events into 5-minute windows before `stats` |
| `sort` | Orders results by one or more fields | Showing rarest/most frequent values first |
| `head` | Limits results to the first N rows | Trimming a long result set, e.g. top 20 rare pairs |
| `dedup` | Removes duplicate events based on a field | Getting one row per unique user/IP |
| `rename` | Renames a field in the results | Making a cryptic field name readable in a table |
| `fields` | Keeps or removes specific fields from results | Trimming unneeded fields before `table`/export |
| `top` | Shows the most common values of a field, with counts | Quick "who/what shows up most" check |
| `rare` | Shows the least common values of a field, with counts | Spotting unusual/rare activity (anomaly hunting) |
| `transaction` | Groups related events into one transaction by shared field(s)/time window | Linking a login attempt and its result across log lines |
| `convert` | Converts a field's data type or format | Turning a raw timestamp string into epoch time |