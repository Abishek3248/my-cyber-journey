# Summary – OWASP Top 10 Vulnerabilities

**In this room, I explored the OWASP Top 10 vulnerabilities, understanding common web application security issues, how they occur, and practical ways to test and mitigate them.**

- Learned about Broken Access Control / IDOR, understanding how improper authorization allows attackers to access other users’ data and how to test for object-level access flaws.
- Explored Cryptographic Failures, including weak hashing, improper encryption, and insecure password storage, and practiced verifying database integrity and cracking weak hashes.
- Studied Injection Vulnerabilities (SQL, Command), learning how user inputs can manipulate backend queries or commands, and practiced exploiting vulnerable parameters safely.
- Understood Insecure Design, including flaws introduced during planning or design phases, and learned the importance of threat modeling and secure development lifecycle (SSDLC).
- Covered Security Misconfigurations, including exposed debug consoles, default credentials, unnecessary services, and learned to test and exploit them practically (e.g., Werkzeug console).
- Learned about Vulnerable and Outdated Components, identifying outdated software versions, searching for public exploits (Exploit-DB), and executing them to understand risks.
- Explored Identification and Authentication Failures, practicing bypasses like re-registration of existing users and understanding session management weaknesses.
- Studied Software and Data Integrity Failures, including missing Subresource Integrity (SRI) checks, manipulating JWTs, and ensuring proper verification of third-party assets and session data.
- Learned the importance of Security Logging and Monitoring, understanding logging practices, monitoring suspicious activity, and how this supports detection and response.
- Explored Server-Side Request Forgery (SSRF), understanding how attackers can coerce servers to send arbitrary requests, enumerate internal networks, and capture sensitive API keys.
- Practiced using practical labs to exploit these vulnerabilities, including database inspection, command execution, JWT tampering, SSRF interception, and exploiting misconfigurations.
- Gained insight into mitigations for each vulnerability, including server-side validation, strong authentication, proper encryption, secure configuration, patching components, and monitoring suspicious activity.
- Built a practical understanding of tools and commands, such as sqlite3, nc, curl, hash functions (md5sum, sha256sum), and browser developer tools to test and analyze vulnerabilities effectively.
