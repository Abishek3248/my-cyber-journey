# Cheatsheet – Packets and Frames

| Concept                 | Description                                                                 | Key Fields / Headers / Notes                                         |
|-------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Packet**              | A unit of data at the Network Layer, containing payload and logical addressing | Contains IP header (Source IP, Destination IP), TTL, Checksum, Data  |
| **Frame**               | Encapsulates packets at the Data Link Layer for physical transmission       | Adds MAC addresses (Source & Destination), frame check sequence (FCS) |
| **Encapsulation**       | Process of wrapping data with protocol information as it moves down layers  | Packet inside a frame; frame inside physical transmission           |
| **TCP Packet**          | Connection-oriented, reliable delivery                                       | Headers: Source Port, Destination Port, Sequence Number, Acknowledgement Number, Flags (SYN, ACK, FIN), Checksum, Data |
| **UDP Packet**          | Connectionless, faster, less reliable                                        | Headers: Source Port, Destination Port, TTL, Checksum, Data          |
| **Port**                | Numerical endpoint to direct data to correct application                    | Range: 0–65535; Standard Ports: HTTP (80), HTTPS (443), FTP (21), SSH (22), SMB (445), RDP (3389) |
| **Three-Way Handshake** | TCP connection establishment process                                         | Steps: SYN → SYN/ACK → ACK                                           |
| **Connection Closure**  | TCP connection termination process                                           | Steps: FIN → FIN/ACK → ACK                                           |
| **TTL (Time to Live)**  | Packet expiration timer to prevent infinite loops in the network            | Decrements at each hop; packet discarded at 0                        |
| **Checksum**            | Error-checking value to ensure data integrity                               | Calculated by sender; verified by receiver                           |
| **Flags**               | Control bits in TCP packets                                                 | Common: SYN (start), ACK (acknowledge), FIN (finish), RST (reset)   |

