# Cheatsheet - Networking Concepts

| Concept                  | Description / Key Points                                                                 |
|---------------------------|----------------------------------------------------------------------------------------|
| OSI Model                 | 7-layer conceptual model: Physical, Data Link, Network, Transport, Session, Presentation, Application. Helps understand networking communication. |
| TCP/IP Model              | Practical model: Application, Transport, Internet, Link (sometimes includes Physical). Maps to OSI layers. |
| IP Address                | Unique identifier for devices. IPv4 = 32-bit (4 octets), IPv6 = 128-bit. Examples: 192.168.1.1 |
| Subnet Mask               | Defines network and host portion of IP address. Example: 255.255.255.0 = /24           |
| Broadcast Address         | Address used to send packets to all hosts in a subnet. Example: 192.168.1.255          |
| Private IP Ranges         | RFC 1918: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16                                   |
| Router                    | Forwards packets between networks, operates at Layer 3, chooses best path for delivery  |
| UDP (User Datagram Protocol) | Connectionless transport protocol, no delivery guarantee, faster. Ports: 1–65535       |
| TCP (Transmission Control Protocol) | Connection-oriented transport protocol, reliable, uses three-way handshake (SYN, SYN-ACK, ACK). Ports: 1–65535 |
| Encapsulation             | Each layer adds header/trailer to data from above layer: Application → Transport → Network → Link → Physical |
| Telnet                    | Protocol for remote terminal connection. Can connect to any TCP port. Examples: Echo (7), Daytime (13), HTTP (80) |
