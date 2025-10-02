# Cybersecurity 101 Path

## What I Learned and Gained
- Through this path, I began building core cybersecurity skills starting with the Command Line module and then progressed to Networking fundamentals. I learned to interact with Linux shells and PowerShell, automate tasks with scripts, gather system and network information, and explore how devices communicate in a network — forming a practical base for further cybersecurity work. The Networking module added hands-on experience with protocols, traffic capture, and secure communication, enhancing my understanding of both local and remote network operations. Completing the Cryptography module further strengthened my skills by teaching me how to securely store and manage passwords, verify data integrity, understand cryptographic keys, and apply encryption concepts in practical cybersecurity tasks. Most recently, the Exploitation Basics module tied those foundations to offensive workflows: discovering vulnerable vectors, using exploit frameworks and payloads, obtaining and stabilizing sessions, and performing principled post-exploitation and evidence collection in authorized lab environments.

## Key Concepts Covered
- Command Line: Linux shell navigation, file operations, basic shell scripting (variables, loops, conditionals), searching with grep/find, PowerShell basics and pipelines, and remote command execution.
- Networking: OSI and TCP/IP models, IP addressing and subnetting, ARP, routing basics, DHCP, NAT, TCP/UDP communication, LAN devices, VLANs, and practical packet flow analysis. Protocol operation (HTTP/HTTPS/FTP/SMTP/POP3/IMAP) and how TLS, SSH, and VPNs secure communications.
- Cryptography: Cryptography fundamentals (confidentiality, integrity, authenticity), symmetric and asymmetric encryption (AES, RSA, Diffie-Hellman), key management, SSH/GPG key workflows, password hashing (bcrypt, scrypt, Argon2, yescrypt), hash recognition and cracking (Hashcat, John the Ripper), data integrity verification (sha256sum), and HMACs for authenticity + integrity.
- Exploitation Basics: exploit lifecycle (recon → vuln ID → exploit → delivery → session → post), RCE/SMB abuse examples (e.g., MS17-010 and file:// moniker netNTLMv2 leakage), Metasploit module structure and payload models (inline vs staged), Meterpreter architecture and extensions, and post-exploitation goals (enumeration, credential extraction, escalation, lateral movement).

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

- running focused scans and NSE scripts to identify vulnerable vectors, using Metasploit (msfconsole, msfvenom, exploit/multi/handler) to select and run modules, generating and delivering payloads, interacting with Meterpreter (migration, hashdump, load kiwi), stabilizing sessions, and performing offline cracking of captured hashes — all practiced with strict lab hygiene and documentation.

## Overall Takeaway
The combination of Command Line, Networking, Cryptography, and Exploitation Basics established a strong, practical foundation for cybersecurity tasks. I can now interact with systems, automate routine tasks, gather and analyze system/network data, secure communications, apply cryptographic principles, and responsibly perform controlled exploitation and post-exploitation workflows in a lab setting. These skills let me both assess systems from an attacker’s perspective and recommend concrete hardening steps — a foundation I will continue to expand as I progress through the rest of the Cybersecurity 101 path.
