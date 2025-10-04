# Summary – OWASP Top 10 Vulnerabilities

**In this room I explored the OWASP Top 10: common web-app security risks, how they arise, how to test for them, and practical mitigations.**

- Broken Access Control / IDOR — learned how missing server-side authorization allows attackers to access other users’ objects and how to test object-level access.
- Cryptographic Failures — covered weak hashing, poor key/transport practices, verifying DB integrity, and cracking weak hashes.
- Injection (SQL / Command) — saw how untrusted input can alter queries/commands and practised exploiting vulnerable parameters safely.
- Insecure Design — understood design-time flaws (e.g., weak rate-limiting) and the need for threat modelling and SSDLC.
- Security Misconfiguration — identified exposed debug consoles, default creds, and other bad defaults; practised exploiting misconfigs (e.g., Werkzeug).
- Vulnerable & Outdated Components — learned to identify old software, search for public exploits (Exploit-DB), and assess risk.
- Identification & Authentication Failures — examined session and auth weaknesses (re-registration bypass, weak session tokens) and mitigation like MFA and lockouts.
- Software & Data Integrity Failures — covered missing SRI, unsafe third-party assets, and JWT tampering; stressed signed packages and integrity checks.
- Security Logging & Monitoring — emphasised logging key events (timestamps, IPs, endpoints, status codes) and detecting anomalous activity.
- SSRF — studied how attackers force server-side requests, enumerate internal services, and capture sensitive endpoints or keys.
