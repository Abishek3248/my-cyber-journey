# Cheatsheet - Networking Secure Protocols

| Protocol | Purpose | Default Port (Insecure) | Default Port (Secure) | Security Mechanism | Notes |
|----------|---------|------------------------|---------------------|------------------|-------|
| TLS      | Provides encryption, confidentiality, and integrity for network protocols | N/A | N/A | Cryptography (TLS 1.3 latest) | Used as a layer to secure multiple protocols like HTTP, SMTP, POP3, IMAP |
| HTTPS    | Secure web browsing | 80 (HTTP) | 443 | TLS | HTTP over TLS encrypts data between browser and server |
| SMTPS    | Secure email sending | 25 (SMTP) | 465 / 587 | TLS | SMTP over TLS protects email in transit |
| POP3S    | Secure email retrieval | 110 (POP3) | 995 | TLS | POP3 over TLS secures email download |
| IMAPS    | Secure email access | 143 (IMAP) | 993 | TLS | IMAP over TLS allows email synchronization across devices securely |
| SSH      | Secure remote access | 23 (TELNET) | 22 | Encryption, authentication, integrity | Provides secure shell, tunneling, X11 forwarding |
| SFTP     | Secure file transfer (over SSH) | 21 (FTP) | 22 | SSH | Unix-like commands, secure alternative to FTP |
| FTPS     | Secure file transfer (over TLS) | 21 (FTP) | 990 | TLS / SSL | Requires TLS certificate; separate control and data connections |
| VPN      | Secure private network over Internet | N/A | N/A | Encryption, tunneling | Connects remote users or offices securely, masks public IP, can route all traffic through tunnel |

