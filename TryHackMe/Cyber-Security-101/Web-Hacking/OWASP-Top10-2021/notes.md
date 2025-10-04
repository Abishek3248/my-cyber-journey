# OWASP Top10 2021

## Introduction
- This room breaks each OWASP topic down and includes details on the vulnerabilities, how they occur, and how you can exploit them. You will put the theory into practice by completing supporting challenges.
  - Broken Access Control
  - Cryptographic Failures
  - Injection
  - Insecure Design
  - Security Misconfiguration
  - Vulnerable and Outdated Components
  - Identification and Authentication Failures
  - Software and Data Integrity Failures
  - Security Logging & Monitoring Failures
  - Server-Side Request Forgery (SSRF)


## Broken Access Control

### Concepts Learned
- Access control ensures users can only access resources and actions they are authorized for.
- Broken Access Control occurs when these restrictions are not properly enforced.
- Insecure Direct Object Reference (IDOR) is a common type of Broken Access Control vulnerability.
- Attackers can exploit IDOR to access or manipulate data belonging to other users.

### Explanation
- Websites often have protected pages meant only for certain users (e.g., admins).
- If unauthorized users can access these pages, the site’s access controls are broken.
**This can allow attackers to:**
  - View sensitive user data.
  - Perform unauthorized actions.
- Example: A 2019 YouTube vulnerability allowed attackers to fetch frames from private videos, violating user privacy expectations.
- IDOR (Insecure Direct Object Reference) happens when applications use user-controlled input (like IDs in URLs) to directly access internal objects without validating permissions.
**Example:**
   - URL: https://bank.thm/account?id=111111 → valid user account.
   - If an attacker changes the ID to 222222, and the site doesn’t check ownership, they could see another user’s details.
   - The issue isn’t with the use of direct object references themselves, but with the lack of proper authorization checks.

### Notes
- Always validate user permissions before granting access to resources.
- Avoid exposing internal identifiers (like numeric IDs) directly in URLs.
- Implement server-side authorization checks for every sensitive request.
- IDOR vulnerabilities are part of the OWASP Top 10 due to their frequency and impact.
- Proper session management and role-based access control help prevent Broken Access Control vulnerabilities.


## Cryptographic Failures

### Concepts learned
- What constitutes a cryptographic failure and why correct use of crypto matters.
- Difference between data in transit and data at rest.
- Practical impact: sensitive-data exposure, MITM risk, and weak storage choices (e.g., flat-file DBs).
- Basic use of sqlite3 to explore downloaded SQLite databases.

### Explanation
- Cryptographic failures occur when sensitive data isn’t properly protected — either through weak, missing, or misused encryption methods.
- Cryptography ensures confidentiality and integrity of data, both while it’s being transmitted and when it’s stored.
- Data in Transit refers to information moving between client and server (e.g., your browser and email server).
- Encryption (like HTTPS/TLS) prevents attackers from intercepting readable data.
- Data at Rest data stored on a server or database.
- Should also be encrypted so that even if compromised, it’s not directly readable.
- Example: encrypted emails stored on a provider’s server.
**Consequences of Cryptographic Failures:**
  - Exposure of personal or financial information (like credit card details).
  - Disclosure of login credentials or passwords.
  - Allows attackers to perform man-in-the-middle (MITM) attacks or exploit unencrypted data.
**Common Scenario:**
  - A web app may accidentally expose its database file under the web root directory.
  - Attackers can directly download and query it if accessible from a browser.
**Flat-file Databases (SQLite):**
  - Often used by smaller web apps.
  - Stored as a single .db file and can be accessed with sqlite3 tool.
  - If stored in the public directory (e.g., /assets/), it becomes downloadable and exposes sensitive data.
**Example Process:**
  - Attacker finds /assets/webapp.db.
**Opens it using:**
  - sqlite3 webapp.db
**Lists tables:**
  - .tables
**Gets table info:**
  - PRAGMA table_info(customers);
**Dumps data:**
  - SELECT * FROM customers;
- Extracts customer names, credit card numbers, and password hashes.
**Cracking Hashes:**
  - Passwords are stored as hashes (e.g., MD5).
  - Using hash-cracking tools (like CrackStation or John the Ripper), the attacker retrieves plaintext passwords (e.g., qwertyuiop).

### Notes
- Cryptographic failures = sensitive data exposure due to weak/missing encryption.
- Always encrypt both data in transit (HTTPS) and data at rest (stored data).
- Never store databases or config files inside the web-accessible directory.
**SQLite databases can be viewed using:**
  - sqlite3 <database-name>


### Challenge (Practical / Lab)
- Objective: Find the exposed DB, extract the admin password hash, crack it, and use it to log in and retrieve the flag.
**High-level steps:**
  - Browse the web app at http://MACHINE_IP:81/.
  - Follow the developer note to the indicated directory.
  - Download the database file found there.
  - Open it with sqlite3 and inspect tables (.tables, PRAGMA table_info(...), SELECT * FROM ...).
  - Extract the admin user’s password hash.
  - Crack the hash offline (John, Hashcat, or online databases) to obtain the plaintext password.
  - Log in as admin and retrieve the flag.
**Findings (from the challenge):**
  - Directory with sensitive data: /assets
  - Suspicious file: webapp.db
  - Admin password hash: 6eea9b7ef19179a06954edd0f6c05ceb
  - Cracked admin password (plaintext): qwertyuiop
  - Next step: use qwertyuiop to log in as admin and collect the flag (retrieve in-app).

### Mitigations
- Never place databases or backups under webroot; store them outside public directories.
- Enforce least privilege for file access on the server.
- Use strong hashing for passwords (bcrypt/Argon2) with salts; avoid fast hashes (MD5/SHA1) for passwords.
- Enforce HTTPS and validate TLS configuration to prevent interception.
- Monitor and audit served files and ensure correct server config prevents accidental exposure.


## Injection

### Concepts learned
- Injection vulnerabilities occur when user-controlled input is interpreted as code, commands, or queries.
- Common injection types: SQL Injection (SQLi) and Command Injection.
- Main defence: ensure user input is never directly executed — use allow-lists, sanitisation libraries, and safe APIs.
- Command Injection can let an attacker run arbitrary OS commands on the server; SQLi can let them manipulate the database.

### Explanation
- Injection flaws happen when an application incorporates untrusted input into a command, query, or interpreter without proper validation or separation. The interpreter treats attacker data as part of the instruction stream.
- Occurs when user input is concatenated into SQL statements.
- An attacker can modify queries to read, modify, or delete data (e.g., dump user table, bypass auth).
- Primary defence: parameterised queries / prepared statements (never concatenate user values into SQL).
**Command Injection:**
  - Happens when server-side code (PHP, Python, etc.) calls system commands and inserts user input into that command line.
  - Example risk: code uses PHP’s passthru() (or exec(), system(), backticks) with untrusted variables → attacker injects payload to run arbitrary OS commands.
  - Consequences: file reading, remote reconnaissance (whoami, id, uname -a), spawning shells, lateral movement.
**Why it works (root cause):**
  - The application builds a command string that includes user input and executes it in a shell context. Shell metacharacters / features (e.g., ;, &&, |, backticks `, or $(...)) allow chaining or embedding further commands.
  - If input is not constrained or escaped, these metacharacters become an injection vector.
**Command Injection example explained:**

**Vulnerable PHP snippet:**
   
    <?php
       if (isset($_GET["mooing"])) {
         $mooing = $_GET["mooing"];
         $cow = 'default';
         if (isset($_GET["cow"])) $cow = $_GET["cow"];
         passthru("perl /usr/bin/cowsay -f $cow $mooing");
         }
     ?>
**Why vulnerable:**
  - $cow and $mooing are concatenated into the shell command without validation or escaping.
  - An attacker can submit payloads containing shell constructs. The shell will execute injected commands before (or instead of) the intended argument.
**Typical injection vectors:**
  - Inline command substitution: $(whoami) or `whoami` — shell executes the inner command and substitutes its output.
  - Command chaining: ; whoami or && cat /etc/passwd — append additional commands.
**Exploitation technique (practical note):**
  - Inject $(COMMAND) or backticks to run commands inline; e.g. sending mooing=$(whoami) may make the application run whoami and include its output.
  - Try reconnaissance commands: whoami, id, uname -a, ps -ef, ip addr / ifconfig.
  - Use the web app entry point (e.g., http://MACHINE_IP:82/) to deliver payloads and observe output.
**Mitigations (general & specific):**
  - Avoid shell calls: use language-native libraries instead of executing shell commands where possible.
  - Allow-list input: accept only expected characters/values (e.g., a known list of cow names).
  - Escape safely: if shell execution is unavoidable, use proper escaping functions (escapeshellarg() / escapeshellcmd() in PHP) — but escaping is brittle; prefer avoiding shells entirely.
  - Least privilege: run services with minimal permissions so even if exploited the impact is limited.
  - Logging & monitoring: detect anomalous commands or output patterns.

### Notes
- Core defences: parameterised queries for SQL; allow-lists and safe APIs for OS actions.
**PHP helpers (if shell unavoidable):**
  - escapeshellarg($arg) — quote/escape a single argument.
  - escapeshellcmd($cmd) — escape an entire command string (use cautiously).
  - Dangerous characters / constructs to watch for: ;, &&, |, >, <, backticks `, $(...).
**Quick payload examples (do not run on targets you don’t own):**
  - Inline substitution: $(whoami) or `whoami`
  - Chaining: ; id or && cat /etc/passwd
  - Lab findings (typical): exploit yields user (apache), shell info (/sbin/nologin), OS details (e.g. Alpine version 3.16.0), or presence of files like drpepper.txt.
  - When testing: use Burp or browser to inject payloads into parameters; capture responses for evidence.
 
### Command Injection — Challenge (Practical / Lab)
- **Objective:** Exploit a vulnerable cowsay endpoint, run OS commands, and gather host info / flags.
- **High-level steps:**
  1. Visit the lab URL (e.g. `http://MACHINE_IP:82/`) and find the cowsay input parameter.
  2. Inject shell payloads using inline substitution or command chaining (e.g. `$(whoami)` , `` `id` ``, `; uname -a`).
  3. Observe command output returned by the application (the cowsay output contains command results).
  4. Use reconnaissance commands (`whoami`, `id`, `ps -ef`, `ip addr`, `uname -a`) to enumerate.
  5. Locate files of interest and capture flags or indicators.

- **Findings (lab results):**
  - Strange file in webroot: `drpepper.txt`
  - Number of non-root/non-service/non-daemon users: `0`
  - Application user: `apache`
  - User shell: `/sbin/nologin`
  - OS / distro info found: Alpine `3.16.0`

- **Tools used:** Browser + manual URL tampering (or Burp Suite for request tampering).  
- **Mitigation reminder:** avoid shell execution from web inputs; use allow-lists or language-native APIs; run services under least privilege.


## Insecure Design

### Concepts learned
- Insecure design = architecture-level security flaws introduced during planning.
- These flaws are harder to fix than coding bugs and often require redesign.
- Example: password-reset flows vulnerable to distributed brute force.

### Explanation
- Definition: Flaws in the application's design or threat model (not just code/config).
- Root cause: Poor threat modelling or dev shortcuts left in production.
**Example (password reset):**
  - Short numeric reset codes + rate limits tied only to IP → attacker can distribute attempts across many IPs (cloud/proxies) and brute-force codes.
  - The problem is the design assumption (attackers won’t have many IPs), not an implementation bug.
  - Why serious: Design issues affect multiple components and are costly to remediate.
  - Prevention (high level): Threat modelling, SSDLC, multi-signal throttling (account + IP + device), high-entropy tokens, MFA.

### Notes
**Short checklist:**
  - Threat-model early.
  - Don’t rely on IP-only rate limits.
  - Use strong, single-use reset tokens bound to account/session.
  - Add CAPTCHA/MFA or progressive friction for suspicious activity.

### Practical — Password-reset lab
- Objective: Find and abuse the reset-design weakness at http://MACHINE_IP:85 to access Joseph’s account.
**Steps:**
  - Inspect reset workflow and token format.
  - Check where rate-limiting applies (IP vs account).
  - Try multiple attempts from different IPs (or simulate) if allowed by lab.
  - Use recovered token/password to log in.
  - What to record: token format, where throttling is applied, and exact remediation suggestions.
 

## Security Misconfiguration

### Concepts learned
- Security misconfiguration happens when safe defaults or settings are not applied.
- It’s a high-impact but often simple class of vulnerability (exposed admin/debug interfaces, default creds, open cloud buckets, missing headers).
- Debugging consoles (e.g. Werkzeug) are especially dangerous if left enabled in production.
- Remediation is primarily correct configuration, least privilege, and hardening.

## Explanation
- Security misconfiguration = components, frameworks, or servers left in insecure default or debug states, or configured with excessive privileges/features.
**Common causes / examples:**
  - Default accounts/passwords still active.
  - Unnecessary services or ports open.
  - Verbose error messages revealing stack traces, paths, or secrets.
  - Debug consoles or REPLs exposed on production URLs (Werkzeug /console, Django debug toolbar, etc.).
  - Publicly accessible backups, database files, or admin panels.
  - Missing HTTP security headers (CSP, HSTS, X-Frame-Options).
**Why it’s dangerous:**
  - Misconfiguration often gives direct, immediate control or sensitive information (e.g., arbitrary code execution via a debug console).
  - It’s a common initial vector that leads to more severe issues (RCE, data leakage, privilege escalation).
**Werkzeug console case :**
  - Werkzeug debug console provides a Python REPL and can execute arbitrary code on the server.
  - If accessible (e.g., http://host/console) an attacker can run OS commands and read source files.
**Prevention :**
  - Disable debug modes and developer consoles in production.
  - Remove unused services and restrict access to admin interfaces (network ACLs, IP allowlists).
  - Harden server configs, rotate default credentials, and enforce least privilege.
  - Implement secure error handling (no stack traces to users).
  - Run periodic configuration audits and automated hardening checks.

### Notes
- Checklist: disable debug, change defaults, remove dev endpoints, apply least privilege, enable security headers.
- Quick mitigations: environment-based config (DEV vs PROD), CI checks to block debug flags, monitoring for unusual endpoints.
- Danger signs to scan for: /console, /debug, /admin, exposed .env, .git or DB files in webroot.

### Practical — Werkzeug console lab
- Objective: Use the exposed Werkzeug debug console to read app source and retrieve the secret flag.
**Key commands used in lab:**
**Run an OS command:**
  - import os
  - print(os.popen("ls -l").read())
**Read a file (example app.py):**
  - import os
  - print(os.popen("cat app.py").read())
**Findings (lab results):**
  - Database filename found: todo.db
  - secret_flag value in source: THM{Just_a_tiny_misconfiguration}
 

## Vulnerable & Outdated Components

### Concepts learned
- Using outdated software/components exposes known vulnerabilities.
- An attacker can research versions and reuse public exploits (Exploit-DB, GitHub, etc.).
- Exploit scripts may need minor fixes; understanding scripting languages helps.
- Mitigation = timely patching, inventory & monitoring of components, and vulnerability management.

### Explanation
- Vulnerable and outdated components are third‑party libraries, frameworks, or services running known vulnerabilities because they were not updated or hardened.
- Publicly disclosed CVEs often come with PoC exploits; an unpatched component is a low-effort, high-impact target.
- Attackers can weaponise existing exploits to gain RCE, data theft, or pivot inside the network.
**Typical discovery workflow:**
  - Identify software/service and version (banner, headers, fingerprinting tools like WPScan/Nmap).
  - Search public sources (Exploit-DB, CVE databases, GitHub) for advisories or exploit code.
  - Test exploit carefully in lab (read usage, required args).
  - If needed, debug/modify exploit script (comment errors, adjust Python2 vs Python3, etc.).
  - Execute against target in authorized environment to confirm impact.
**Practical notes on exploit scripts:**
  - Scripts often include usage comments and required parameters.
  - They may assume an interpreter (python2 vs python3); errors are common and usually fixable.
  - Always review code before running; understand what it does.
**Mitigations**
  - Maintain inventory of all components and versions.
  - Regular patching schedule and risk-based prioritisation.
  - Apply virtual patching / WAF rules when immediate patching isn’t possible.
  - Use security scanners and subscribe to vendor/CVE alerts.

### Notes
- Quick checklist: identify version → search CVE/Exploit-DB → test in lab → patch/update.
- When running public exploits: read comments, fix minor script issues, ensure correct interpreter.
- Defence: timely patching, component inventory, automated scanning.

### Practical — Lab
- Target: http://MACHINE_IP:84 (vulnerable Nostromo 1.9.6 in this exercise).
- Approach: find service/version → search Exploit-DB → download exploit script → fix trivial script bug (comment stray line) → run with proper interpreter (e.g., python2 47837.py <host> <port> <cmd>).
- Result / finding: Remote code execution achieved; flag contents in /opt/flag.txt:
- THM{But_1ts_n0t_my_f4ult!}


## Identification & Authentication Failures

### Concepts learned
- Authentication/ session management are critical — flaws let attackers impersonate users.
- Common issues: brute force, weak passwords, predictable session tokens, and logic flaws.
- Defenses: strong passwords, account lockouts/rate-limiting, MFA, secure session tokens, input validation.

### Explanation
- failures in how an application identifies users (auth) or maintains identity across requests (sessions).
- attackers who break auth can access other users’ data, perform actions as them, or escalate privileges.
**Common vectors:**
  - Brute-force / credential stuffing: no throttling or weak password policies.
  - Weak session tokens: predictable or unprotected cookies allow session forgery.
  - Re-registration / logic flaws: the app accepts visually different usernames (e.g. leading space) as distinct accounts but grants them the same privileges.
  - SQLi or injection in auth flows: unsanitised inputs let attackers bypass checks.
**Mitigations (high level):**
  - Enforce strong password policies and lockouts / exponential backoff.
  - Implement MFA and device/session binding.
  - Use cryptographically secure, long, random session tokens (HttpOnly, Secure, SameSite).
  - Canonicalise/normalise usernames and validate input to prevent dupes with differing whitespace/encodings.
  - Log and alert on suspicious auth patterns.

### Notes
- Short checklist: rate-limit logins, require MFA, normalise usernames, use secure cookies, enforce strong passwords.
### Practical — Re-registration lab
- Objective: exploit a logic flaw where registering a username with trivial whitespace creates a new account that maps to an existing user’s privileges.
**Steps**:
  - Visit http://MACHINE_IP:8088.
  - Try to register an existing username (e.g., darren) — registration is blocked.
  - Register with a visually different username that includes a leading space (e.g., " darren").
  - The app creates a new account but shows darren’s content / privileges (no canonicalisation).
  - Repeat for other users (e.g., arthur).
**Lab findings:**
  - Flag found in darren's account: fe86079416a21a3c99937fea8874b667
  - Flag found in arthur's account: d9ac0f7db4fda460ac3edeb75d75e16e
  - Mitigation note: normalise usernames (trim whitespace, apply unicode normalization), prevent duplicate privilege assignment, and add server-side checks to avoid visually distinct but equivalent identifiers.
 

## Software & Data Integrity Failures

### Concepts learned
- Integrity = ability to detect unauthorised modification of software or data.
- Two classes: software integrity failures (tampered third‑party code) and data integrity failures (trusting client‑modifiable data).
- Mitigations: Subresource Integrity (SRI), signed releases/artifacts, cryptographic signatures, and server‑side integrity checks (don’t trust client data).

### Explanation

**Software integrity failures**
  - Web apps that pull libraries or executables from external servers must verify those artifacts (hashes/signatures).
  - Example risk: loading a compromised CDN JS file injects malware into every visitor’s browser.
  - Mitigation: use Subresource Integrity (SRI) for web assets and verify checksums/signatures for downloaded software.
**SRI example:**
<script src="https://code.jquery.com/jquery-3.6.1.min.js"
        integrity="sha256-…"
        crossorigin="anonymous"></script>
- Lab fact: SHA‑256 for https://code.jquery.com/jquery-1.12.4.min.js (SRI form): sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=
**Data integrity failures**
  - Storing trustable state in client‑controlled fields (cookies, localStorage, URL params) without integrity checks allows tampering.
  - JWTs are common: header.payload.signature — the signature enforces integrity.
  - Vulnerable libraries or bad verification logic may accept alg: none and skip signature checks, letting an attacker modify payloads (e.g., escalate to admin).
  - Mitigation: validate signatures, reject alg:none, use server‑side session state or signed tokens with robust algorithms and secret management.
**JWT None Attack** 
- Decode header & payload (base64), change "alg" to "none", alter payload (e.g., "username":"admin"), re‑encode header.payload and remove signature (leave trailing dot if required by app).
- If server accepts alg:none without checking allowed algorithms, the attacker gains forged privileges.

### Notes
**Short checklist**
  - Verify third‑party code with SRI or signed releases.
  - Verify download checksums (MD5/SHA* only for integrity; use signatures for authenticity).
  - Don’t trust client data — validate or sign it server‑side.
  - Reject insecure JWT algs (none), enforce algorithm allow‑lists, rotate secrets, and use exp/nbf claims properly.

### Practical — JWT None attack
**Goal**
  - Forge the jwt-session cookie so the app thinks you are admin and retrieve the admin flag.
**Pre‑req**
  - Log in as guest (password guest) so the site issues a JWT cookie.
  - Login as guest at http://MACHINE_IP:8089/.
  - Open Developer Tools → Application (Cookies) or Storage → find cookie named jwt-session. Copy its value (the token).
  - Split token into three parts header.payload.signature (dots). Use an online base64url tool or browser console to decode header & payload.
  - Edit header JSON: change "alg":"HS256" (or similar) → "alg":"none".
  - Edit payload JSON: change "username":"guest" → "username":"admin".
  - Base64url‑encode the modified header and payload (no padding), join as:
  - new_token = base64url(header) + '.' + base64url(payload) + '.'
**Replace cookie value: in console:**
  - document.cookie = "jwt-session=NEW_TOKEN; path=/;"; 
  - Reload the page — you should be logged in as admin. Capture the admin flag.


## Security Logging and Monitoring Failures

### Concepts learned
- Logging is essential to trace attacker actions and support incident response.
- Monitoring converts logs into detection (alerts) so incidents are discovered quickly.
- Missing/poor logging makes breach impact unknown and blocks remediation & forensics.
- Not all alerts are equal — triage by impact (high/medium/low) is required.

### Explanation
**Why logging matters**
  - Logs provide an audit trail of user and system activity (who did what, when, where).
  - Regulators and incident responders rely on logs for investigation and legal obligations.
  - Without logs you can’t determine scope, timeline, or method of a breach.
**What to log**
  - Timestamp (UTC) and timezone.
  - Source IP address (and X‑Forwarded‑For when behind proxies).
  - Username / account identifier.
  - Action/event type (login, file access, admin action, API call).
  - Target resource or endpoint (URL, file path, API route).
  - HTTP status codes and response size.
  - User-Agent and other request headers (when relevant).
  - Session ID / correlation ID / request ID for tracing.
  - Error messages and stack traces (but avoid leaking secrets).
  - Outcome (success/failure) and reason for failure (e.g., invalid token).
**Monitoring & detection**
  - Monitoring = automated analysis of logs to detect anomalies and known bad patterns.
  - Examples of suspicious patterns: repeated failed logins, sudden privilege use, many requests from one IP, unusual geographic access, high request rate (bots), known exploit payloads.
  - Use baselining (normal behaviour) to reduce false positives.
  - Alerts must be actionable (include context: affected user, time, IP, evidence).
**Retention, protection & integrity**
  - Store logs immutably (or write-once) and off-host to prevent attacker tampering.
  - Keep multiple copies (separate storage / SIEM) and enforce access controls.
  - Define retention based on business/legal needs (e.g., 90 days active, archive longer).
  - Sign or checksum critical logs to detect tampering.
**Triage & response**
  - Classify alerts by severity and impact; route high-severity to incident response immediately.
  - Include playbooks for common alerts (credential compromise, data exfiltration attempts).
  - Enrich logs with threat intel (bad IP lists, user risk scores) to prioritize.

### Notes
**Quick checklist**
  - Log all auth events (login success/fail, password reset, MFA events).
  - Log admin actions and privilege escalations.
  - Ensure timestamps are synchronized (NTP) and in UTC.
  - Forward logs to a central SIEM or log store (don’t keep only local files).
  - Protect logs from deletion by limiting write/delete access to a few accounts.
  - Mask or redact sensitive data in logs (PII, full credit cards, secrets).
  - Create and test alerting/playbooks for high‑risk events.
**Examples of high‑priority alerts**
  - Multiple failed login attempts followed by a successful login.
  - Login from a high‑risk country for a user who normally logs in from one country.
  - Creation of new admin/privileged accounts.
  - Unexpected outbound data transfer spikes (possible exfil).
  - Web application errors that reveal stack traces or SQL errors repeatedly (possible probing).
**practical tip for labs**
- If an app lacks logging, add quick instrumentation: log auth attempts and admin actions to a file, then forward that file into a centralized viewer (elastic/Graylog). This makes incidents discoverable during exercises.


## Server‑Side Request Forgery (SSRF)

### Concepts learned
- SSRF = attacker makes the server perform HTTP/other requests on their behalf.
- Impacts range from data leakage to internal service access and cloud credential theft.
- Two useful SSRF types: direct (response visible) and blind (no immediate response).

### Explanation
- App accepts a user-controlled URL/host and the server fetches it → attacker controls destination.
- Dangerous because servers can reach internal/trusted services (localhost, private IP ranges, cloud metadata).
- Common abuses: retrieve internal APIs, exfiltrate API keys, probe internal ports, access cloud metadata (e.g., 169.254.169.254).
- Simple defenses: allowlist outbound hosts, block private ranges, disallow unsafe schemes, and enforce egress firewall rules.
- Always validate the final resolved IP (after DNS + redirects) before allowing the request.

### Notes
**quick checklist**
  - Deny private IP ranges by default (127.0.0.0/8, 10.0.0.0/8, 169.254.169.254, etc.).
  - Use server-side allowlist of trusted domains only.
  - Enforce network egress rules (firewall/ACL) so app servers cannot reach management/metadata endpoints.
  - Strip sensitive headers and never put secrets in URLs.
  - Log and alert on outbound requests to unusual destinations.

### Practical Lab
**Target app behaviour**
  - App had a parameter that defined the remote host used for fetching files (server parameter).
  - Admin area restricted to requests coming from localhost.
**Steps I used to exploit**
  - Set up a listener on my machine (e.g. nc -lvp 80) to capture outbound requests.
  - Replace the server parameter with my AttackBox IP / hostname to force the app to call my listener.
  - Inspect incoming request to capture headers/body and any secrets (API keys, tokens).
  - Probe internal endpoints by changing server to 127.0.0.1, 10.x.x.x, 169.254.169.254, or other private ranges.
  - Try alternative schemes/ports (if client supports them) for non‑HTTP services.
**Lab results / findings**
  - Allowed admin host: localhost.
  - Original server parameter pointed to: secure-file-storage.com.
  - Intercepted API key when redirecting requests to my listener: THM{Hello_Im_just_an_API_key}.


## Key Takeaways
- Web app security is holistic: bugs, design decisions, configuration, and dependencies all matter.
- Validate and enforce authorization on every request — never trust client-side checks (prevent IDOR / broken access control).
- Always treat user input as untrusted: use parameterized queries / prepared statements and proper input handling to prevent injection.
- Use strong, current cryptography for data in transit and at rest; never invent your own crypto or rely on weak/obsolete algorithms.
- Protect secrets and credentials: don’t expose databases, config files, or cloud metadata to unauthorised requests.
- Harden authentication & sessions: enforce strong passwords, MFA, account lockout, secure cookie flags, and unpredictable session IDs.
- Keep components up to date and track third‑party dependencies; known‑vulnerable software massively lowers the effort to compromise.
- Apply integrity checks (SRI, signed packages, checksums) for third‑party code and validate data origins (prevent supply‑chain & tampering attacks).
- Lock down SSRF and outbound requests: allowlist destinations, block private ranges, disable unsafe schemes, and use egress controls.
- Remove or secure debug/management interfaces and fix security misconfigurations before deployment (least privilege + secure defaults).
- Implement robust logging, centralized monitoring and alerting for high‑risk events; logs must be protected and actionable.
- Defence in depth: combine input validation, network controls, proper auth, monitoring, and least privilege — no single control is enough.
- Always validate fixes with tests and repeatable lab exercises — practical exploitation + remediation verification is essential.
