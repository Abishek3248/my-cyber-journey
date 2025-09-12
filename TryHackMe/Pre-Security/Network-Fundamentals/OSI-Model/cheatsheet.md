# Cheatsheet - OSI Model

| Layer (No.)               | Function / Responsibility                                                   | Examples / Notes                                                     |
|---------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Physical (L1)**         | Transmits raw bits (0s and 1s) over physical medium                         | Ethernet cables, Wi-Fi, fiber optics, hubs                           |
| **Data Link (L2)**        | Node-to-node delivery; uses MAC addresses, frames, and error detection      | Devices: Switches, NICs → Frame forwarding                          |
| **Network (L3)**          | Logical addressing (IP), routing, path determination                       | Devices: Routers; Protocols: IP, ICMP, OSPF, RIP                     |
| **Transport (L4)**        | End-to-end communication; ensures reliability (TCP) or speed (UDP)          | **TCP**: reliable, accurate (web, email). **UDP**: fast, best-effort (gaming, streaming) |
| **Session (L5)**          | Establishes, manages, and terminates communication sessions                | Examples: Remote desktop, web logins; supports checkpoints/recovery  |
| **Presentation (L6)**     | Data translation, encryption, compression                                  | Examples: JPEG, MP3, SSL/TLS; ensures receiver can interpret data    |
| **Application (L7)**      | Closest to users; defines how apps interact with network services           | Protocols: HTTP, HTTPS, DNS, FTP, SMTP, POP3; Examples: browsers, email clients |

