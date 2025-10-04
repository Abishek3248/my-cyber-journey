# Cheatsheet — OWASP Top 10

## Essentials

| **Topic** | **One-Line Summary** |
|------------|----------------------|
| **Broken Access Control / IDOR** | Don’t trust client-side access checks — verify ownership/permissions on every request. |
| **Cryptographic Failures** | Use modern algorithms, encrypt in transit & at rest, don’t roll your own crypto. |
| **Injection (SQL / Command)** | Treat all input as untrusted; use parameterized queries / safe APIs. |
| **Insecure Design** | Design phase mistakes (e.g. poor rate limits) are hard to fix later — threat model early. |
| **Security Misconfiguration** | Remove debug consoles, default creds; use secure defaults. |
| **Vulnerable/Outdated Components** | Keep dependencies updated; monitor CVEs and exploit DBs. |
| **Identification & Auth Failures** | Hardening: MFA, lockouts, strong session tokens, unpredictable cookies. |
| **Software & Data Integrity** | Use SRI, signed packages, and verify integrity of third-party assets. |
| **Logging & Monitoring** | Log auth events, IPs, endpoints, timestamps, HTTP status codes; centralize & protect logs. |
| **SSRF** | Validate/allowlist outbound destinations; block private metadata endpoints. |


## Quick Commands & Tools

| **Command / Tool** | **Purpose / Usage** |
|--------------------|---------------------|
| `sqlite3 example.db` | Open & query a flat SQLite DB (`.tables`, `PRAGMA table_info(table)`, `SELECT * FROM table;`). |
| `md5sum` / `sha1sum` / `sha256sum file` | Compute file hashes for integrity checks. |
| `nc -lvp 80` | Start a listener to capture incoming HTTP/SSRF requests. |
| `curl -v 'http://target/?param=...'` | Test HTTP endpoints and injectable parameters. |
| `python2 exploit.py <target> <port> <cmd>` | Typical pattern for running public exploit scripts (read usage in header). |
| **Browser DevTools → Application → Cookies** | Inspect/modify JWT or session cookies for testing auth flaws. |
| `base64 -d` / online Base64 tools | Decode JWT parts (`header.payload.signature`). |
| **Regex / text editors** | Extract IDs, tokens, cookie names, URLs from responses. |


## Quick Tests / Exploit Steps (by Vulnerability)

| **Vulnerability** | **Quick Test / Exploit Steps** |
|-------------------|--------------------------------|
| **IDOR (Insecure Direct Object Reference)** | 1️ Find object ID in URL (`?id=111`). 2️ Modify to another ID (`?id=222`). 3️ If accessible, record sensitive data leakage. |
| **Cryptographic Failures (Exposed DB)** | 1️ Download `webapp.db`. 2️ Use `sqlite3` → `.tables` → `PRAGMA table_info(...)` → `SELECT * FROM ...;`. 3️ Crack hashes using Hashcat/John. |
| **Command Injection (Cowsay Example)** | 1️ Find param used in system call. 2️ Inject: `$(whoami)` → `?mooing=$(whoami)`. 3️ Check output. |
| **SQL Injection** | Use payloads: `' OR '1'='1' --`, `UNION SELECT ... --`; observe response changes/errors. |
| **Werkzeug Debug Console (Misconfiguration)** | Visit `/console`, run `import os; print(os.popen("ls -l").read())` → view files → `cat app.py`. |
| **Outdated Components (Exploit-DB)** | Identify service/version (e.g. *Nostromo 1.9.6*). Search Exploit-DB, adjust and run exploit. |
| **Re-Registration Auth Bypass** | Register username with subtle whitespace (`darren `) to bypass check. |
| **JWT None Algorithm Attack** | Decode JWT → change header to `"alg":"none"`, payload to `{"username":"admin"}` → re-encode → remove signature part. |
| **Software Integrity (SRI Test)** | Check `<script src="...">` tags for missing integrity attributes; use `sha256sum` to compute expected hash. |
| **SSRF (File Download Proxy Example)** | 1️ Find fetch param. 2️ Replace with `http://<your-ip>:80` and listen using `nc`. 3️ Probe internal IPs (127.0.0.1, 10.x.x.x, 169.254.169.254). |


## Common Payloads / Examples

| **Type** | **Example Payload / Input** |
|-----------|-----------------------------|
| **Cowsay Inline Command** | `?mooing=$(whoami)` or `?mooing=$(id)` |
| **IDOR Probe** | Change `?id=111111` → `?id=222222` |
| **JWT None Header** | Header: `{"typ":"JWT","alg":"none"}` Payload: `{"username":"admin"}` → base64(header).base64(payload). |
| **SQL Test** | `' OR '1'='1' --` or `UNION SELECT NULL,NULL,...` |
| **SSRF Local Metadata** | `http://169.254.169.254/latest/meta-data/` |


## Mitigations (Short Checklist)

| **Vulnerability** | **Key Mitigations** |
|--------------------|--------------------|
| **IDOR / Access Control** | Enforce server-side authorization on every object; validate ownership. |
| **Injection (SQL / Command)** | Use prepared statements / parameterized queries; sanitize inputs. |
| **Cryptography** | Enforce TLS, use modern algorithms (AES-256, SHA-256+), secure key management. |
| **JWT / Token Integrity** | Use HS256/RS256, validate algorithm isn’t `none`, rotate secrets. |
| **SRI / Supply Chain** | Use Subresource Integrity for JS/CDN, verify signed package releases. |
| **Debug Consoles** | Disable in production; restrict to internal/dev use only. |
| **Outdated Components** | Maintain dependency inventory, patch regularly, track CVEs. |
| **Authentication** | Enforce MFA, strong password policies, account lockouts, secure cookies (`HttpOnly`, `Secure`, `SameSite`). |
| **SSRF** | Allowlist outbound hosts, block internal/private ranges, validate post-DNS resolution. |
| **Logging & Monitoring** | Log auth attempts, IPs, endpoints, status codes; protect & centralize logs; alert on anomalies. |

