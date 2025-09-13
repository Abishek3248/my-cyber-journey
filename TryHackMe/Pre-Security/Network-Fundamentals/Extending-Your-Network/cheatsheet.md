# Cheatsheet - Extending Your Network & Practical Labs

| Topic / Tool          | Description                                                                                  | Example / Notes                                                      |
|-----------------------|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Port Forwarding**    | Allows external devices to access internal network services                                  | Forward port 80 to internal web server 192.168.1.10                  |
| **Firewall**           | Controls network traffic; permits or blocks packets based on rules                            | Stateful: inspects full connection, Stateless: inspects individual packets |
| **DROP Action**        | Firewall action to silently discard packets                                                  | Block malicious traffic to port 80 on 203.0.110.1                     |
| **VPN (Virtual Private Network)** | Creates secure tunnel between networks over the Internet                               | Connects two offices securely; encrypts traffic                       |
| **Router**             | Connects multiple networks, routes packets using IP addresses                                 | Layer 3 device; configures rules like port forwarding                 |
| **Switch**             | Connects multiple devices within a LAN                                                      | Layer 2: forwards frames using MAC addresses; Layer 3: can route IP traffic |
| **VLAN**               | Virtually segments a network for security or organizational purposes                          | Separates Sales and Accounting within same switch                     |
| **TCP Handshake**      | Ensures reliable connection before sending data                                              | SYN → SYN/ACK → ACK                                                   |
| **ARP (Address Resolution Protocol)** | Resolves IP addresses to MAC addresses for local communication                  | `arp -a` shows MAC mapping for devices                                 |

