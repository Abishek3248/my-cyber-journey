# Web Hacking Module — README

## What I Learned and Gained
- Through this module I built a practical, hands-on foundation in web application security: how web clients and servers interact, where vulnerabilities commonly appear, and how to safely discover and validate them in an authorized lab. I gained both conceptual understanding (HTTP, auth/session design, supply-chain integrity) and practical skills (HTTP tooling, Burp workflows, DB inspection, JS analysis, and OWASP Top-10 testing) that let me reproduce issues and recommend concrete mitigations.

## Key Concepts Covered
- HTTP & URL fundamentals — request/response structure, methods (GET/POST/PUT/DELETE/etc.), headers, status codes, URL anatomy (scheme, host, port, path, query, fragment) and how they affect security and routing.
- Content types & request bodies — URL-encoded, multipart/form-data, JSON, XML and their parsing/validation implications.
- Client vs server trust model — why client-side checks are insufficient and server-side validation/authorization is mandatory.
- JavaScript delivery & risks — embedding (internal/external), dialog functions, control flow bypasses, minification/obfuscation, and secure practices (no secrets in client code, vet third-party libs).
- Security headers & hardening — CSP, HSTS, X-Content-Type-Options, Referrer-Policy and their roles in mitigating XSS, clickjacking and data leakage.
- Relational & flat-file DBs — tables/rows/columns, primary/foreign keys, CRUD, clauses/operators, and SQLite risks when DB files are exposed.
- Injection classes — SQL injection, command injection (inline command abuse) and safe mitigations (parameterised queries, avoid direct shell calls).
- OWASP Top-10 coverage — Broken Access Control/IDOR, Cryptographic Failures, Injection, Insecure Design, Security Misconfiguration, Vulnerable Components, Auth failures, Integrity failures (SRI/JWT), Logging & Monitoring, SSRF — origins, testing approaches, and mitigations.
- Integrity & supply-chain — Subresource Integrity (SRI) for CDN JS, signed packages, JWT signing pitfalls (alg=none) and secure token handling.
- SSRF impact — forcing server requests, internal network enumeration, and exfiltration of API keys or metadata endpoints.
- Detection & defensive thinking — logging/monitoring requirements, what to capture (timestamps, IPs, endpoints, status codes), and alerting strategies.

## Practical Skills
- Configured and used Burp Suite effectively: proxying (CA install), FoxyProxy/Burp Browser, scoping, intercept/edit/forward, site map, Repeater and Intruder for manual and semi-automated testing.
- Crafted, inspected and manipulated raw HTTP requests/responses (headers, cookies, bodies) to test functionality and security.
- Performed client-side testing with browser DevTools / console: run JS, inspect/modify cookies, debug client logic, and analyze minified/obfuscated scripts.
- Located and analysed exposed SQLite database files: download → sqlite3 → .tables, PRAGMA table_info, SELECT *, and exported password hashes for cracking.
- Tested authorization flaws (IDOR): identified direct object references and verified ownership checks by manipulating IDs and parameters.
- Identified cryptographic weaknesses: located weak hashes, exported them, and validated cracking approaches using appropriate tools/wordlists.
- Exploited injection issues safely: demonstrated SQL injection probes and command injection (e.g., cowsay passthru inline commands) in lab environments.
- Discovered and exploited security misconfigurations (exposed debug consoles like Werkzeug) to retrieve source or sensitive artifacts in a controlled lab.
- Validated integrity controls: checked for missing SRI, manipulated JWTs (alg header tampering / none attack) to understand token integrity failures.
- Implemented SSRF testing workflows: identify external resource parameters, point them to a listener (nc) to capture requests, and probe internal network endpoints.
- Applied defensive recommendations during testing: record evidence, minimise impact, and propose mitigations (server-side checks, secure headers, SRI, signed tokens, patching, MFA, logging).

## Overall Takeaway
- This module connected web fundamentals to real attacker techniques: mastering HTTP, JavaScript behaviour, and basic database skills is essential before you can reliably find and reproduce web vulnerabilities. Practical fluency with a proxy tool (Burp), browser DevTools, and simple command/DB tooling enables effective testing across the OWASP Top-10. I learned to perform methodical, repeatable checks (intercept → modify → verify → document) and to translate findings into actionable remediations: enforce server-side validation/authorization, adopt secure crypto and integrity checks, harden configurations, patch dependencies, and build logging/monitoring to detect and respond to misuse. All work was done following safe lab practices and with documentation suited for reporting and remediation planning.
