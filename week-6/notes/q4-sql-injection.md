# Q4: SQL Injection

## Types and payload examples

| Type | Description | Example payload |
|---|---|---|
| In-band (UNION-based) | Results returned directly in the app's response | `1' UNION SELECT version(), database()-- -` |
| In-band (error-based) | Forces a DB error that leaks info | `'` (single quote, breaks the query) |
| Blind (boolean-based) | No data shown, but app behaves differently (true vs false) | `1' AND 1=1-- -` vs `1' AND 1=2-- -` |
| Blind (time-based) | App behaves identically, but response is delayed when condition is true | `1' AND IF(1=1,SLEEP(5),0)-- -` |

## Prevention
- **Prepared statements / parameterized queries:** The query structure is fixed at compile time; user input is always treated as data, never as part of the SQL syntax, so a quote or SQL keyword in input can't change the query logic.
- Additional layers: least-privilege DB accounts, input validation, generic error messages (no raw DB errors shown to users).

## How this shows up in my lab
I confirmed in-band SQLi on DVWA's SQL Injection module at Low: a single quote broke the query (HTTP 500), and a UNION payload extracted the MariaDB version and database name directly in the page output. At Medium, the quote payload still broke the query but a quote-free UNION attempt showed no confirmed extraction — the filtering changed the failure mode without fully fixing the root cause.