# Cybersecurity 101 Path

## What I Learned and Gained
- Through this path, I began building core cybersecurity skills starting with the Command Line module and then progressed to Networking fundamentals. I learned to interact with Linux shells and PowerShell, automate tasks with scripts, gather system and network information, and explore how devices communicate in a network — forming a practical base for further cybersecurity work. The Networking module added hands-on experience with protocols, traffic capture, and secure communication, enhancing my understanding of both local and remote network operations. Completing the Cryptography module further strengthened my skills by teaching me how to securely store and manage passwords, verify data integrity, understand cryptographic keys, and apply encryption concepts in practical cybersecurity tasks. Most recently, the Exploitation Basics module tied those foundations to offensive workflows: discovering vulnerable vectors, using exploit frameworks and payloads, obtaining and stabilizing sessions, and performing principled post-exploitation and evidence collection in authorized lab environments. I have now also completed the Web Hacking module, which connected HTTP/URL fundamentals, JavaScript behaviour, and database concepts to OWASP Top-10 testing using tools like Burp Suite and browser DevTools — enabling me to find, validate and suggest mitigations for common web vulnerabilities in a controlled lab.

## Key Concepts Covered
- **Command Line:** Linux shell navigation, file operations, basic shell scripting (variables, loops, conditionals), searching with grep/find, PowerShell basics and pipelines, and remote command execution.
- **Networking:** OSI and TCP/IP models, IP addressing and subnetting, ARP, routing basics, DHCP, NAT, TCP/UDP communication, LAN devices, VLANs, and practical packet flow analysis. Protocol operation (HTTP/HTTPS/FTP/SMTP/POP3/IMAP) and how TLS, SSH, and VPNs secure communications.
- **Cryptography:** Cryptography fundamentals (confidentiality, integrity, authenticity), symmetric and asymmetric encryption (AES, RSA, Diffie-Hellman), key management, SSH/GPG key workflows, password hashing (bcrypt, scrypt, Argon2, yescrypt), hash recognition and cracking (Hashcat, John the Ripper), data integrity verification (sha256sum), and HMACs for authenticity + integrity.
- **Exploitation Basics:** exploit lifecycle (recon → vuln ID → exploit → delivery → session → post), RCE/SMB abuse examples (e.g., MS17-010 and file:// moniker netNTLMv2 leakage), Metasploit module structure and payload models (inline vs staged), Meterpreter architecture and extensions, and post-exploitation goals (enumeration, credential extraction, escalation, lateral movement).
- **Web Hacking:** HTTP/URL anatomy, request/response structure, headers and common content types, JavaScript delivery and client-side risks (dialogue functions, obfuscation), Burp Suite proxy workflows (intercept, scope, site map, Repeater), SQLite/flat-file DB inspection, OWASP Top-10 testing (IDOR, injection, authz/authn, crypto/ integrity failures, SSRF, misconfigurations), and basic mitigations such as server-side validation, SRI, secure JWT handling, and security headers.

## Practical Hands-On Skills
- Navigating and managing files and directories in Linux and Windows.
- Writing and executing shell and PowerShell scripts for automation.
- Collecting system and network data (systeminfo, ipconfig, netstat, etc.).
- Filtering and processing command output (pipes, filters, selective properties).
- Executing commands on remote hosts and using CLI for troubleshooting.
- Performing host discovery and port scanning with Nmap (and db_nmap integration).
- Capturing and analyzing network traffic with Wireshark and Tcpdump; following sessions and interpreting network metadata.
- Observing TCP/UDP streams and testing secure communication via TLS, SSH, and VPNs.
- Generating, managing, and using cryptographic keys (SSH/GPG); recognizing, hashing, and cracking passwords using Hashcat and John the Ripper.
- Verifying file integrity, using HMACs, and checking downloaded files against official hashes.
- Running focused scans and NSE scripts to identify vulnerable vectors, using Metasploit (msfconsole, msfvenom, exploit/multi/handler) to select and run modules, generating and delivering payloads, interacting with Meterpreter (migration, hashdump, load kiwi), stabilizing sessions, and performing offline cracking of captured hashes — all practiced with strict lab hygiene and documentation.
- configure and use Burp proxy and Burp Browser (FoxyProxy/CA import), intercept/edit/forward HTTP requests, map site structure, use Repeater/Intruder for testing, inspect and modify cookies/JWTs in DevTools, download and query exposed SQLite DBs, craft and validate XSS/IDOR/SQL/command injection/SSRF probes in lab, and check/interpret security headers and SRI.

## Overall Takeaway
- The combination of Command Line, Networking, Cryptography, Exploitation Basics and Web Hacking established a broad, practical foundation for core cybersecurity tasks. I can now interact with systems, automate routine tasks, gather and analyze system/network data, secure communications, apply cryptographic principles, and responsibly perform controlled web and host exploitation and post-exploitation workflows in lab settings. These skills let me assess systems from an attacker’s perspective and recommend concrete hardening steps — a foundation I will continue to expand as I progress through the rest of the Cybersecurity 101 path.
