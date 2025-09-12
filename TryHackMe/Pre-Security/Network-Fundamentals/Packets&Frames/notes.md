# Packets & Frames

## Introduction
- In networking, data is not transmitted as a single large stream but is broken into smaller units for efficient delivery. These units are known as packets and frames. While often confused, they operate at different layers of the OSI model and serve distinct purposes in communication.

## What are Packets and Frames?

### Concepts Learned
- Packets belong to the Network Layer (Layer 3) and include IP addressing.
- Frames belong to the Data Link Layer (Layer 2) and include MAC addressing.
- Encapsulation wraps data with multiple headers to ensure proper delivery.
- Splitting data into smaller packets improves efficiency and reduces congestion.

### Explanation
- Packet (L3): Contains payload + IP header (logical addressing).
- Frame (L2): Encapsulates a packet and adds MAC addresses for local delivery.
- Analogy: Frame = envelope, Packet = letter inside. The frame moves the packet; once opened, the packet is processed further.
- Encapsulation: Each layer adds its own header information before transmission.
- Efficiency: Data (e.g., an image) is divided into multiple packets and reassembled at the destination.
- Standardization: Protocols define packet structures to maintain interoperability across devices.

### Notes
- Packets = Network Layer, IP-based, routed across networks.
- Frames = Data Link Layer, MAC-based, delivered within local networks.
- Encapsulation ensures structured delivery through the OSI layers.
- *Packet headers include:*
    - Time to Live (TTL): Prevents infinite looping of packets.
    - Checksum: Validates data integrity.
    - Source Address: IP of the sender.
    - Destination Address: IP of the receiver.
 

## TCP/IP (Three-Way Handshake)

### Concepts Learned
- TCP/IP has 4 layers: Application, Transport, Internet, Network Interface.
- Works similarly to OSI with encapsulation/decapsulation.
- TCP is connection-oriented and reliable (guarantees delivery).
- Establishes a connection using the Three-Way Handshake.
- Uses sequence numbers and acknowledgements to keep data in order.
- TCP connection must be properly closed to free system resources.

### Explanation
- TCP vs OSI: TCP/IP is a simplified 4-layer model (Application, Transport, Internet, Network Interface).
- Connection-based: TCP establishes a session before sending data, ensuring reliability.
- Reliability features: Sequencing, acknowledgements, retransmission, and integrity checking (checksum).
- Encapsulation: Headers are added at each layer; reversed during decapsulation.
- Headers include: Source/Destination Ports, IPs, Sequence Number, Acknowledgement Number, Checksum, Flags, Data.

### Three-Way Handshake Steps
- SYN: Client sends initial sequence number (ISN) to start connection.
- SYN/ACK: Server replies with its ISN + acknowledgement of client’s ISN.
- ACK: Client acknowledges server’s ISN, connection established.
- DATA: Transmission of actual data begins.
- FIN: Connection closed gracefully after data exchange.
- RST: (If needed) Terminates connection abruptly due to errors/issues.
**Sequence Numbers**
- Data starts with a random Initial Sequence Number (ISN).
- Each new packet increments by +1 to maintain correct order.
- Both client and server must agree on sequence numbers during handshake.
**Closing TCP Connection**
- Device sends FIN → other device acknowledges.
- Other device also sends FIN → first device acknowledges.
- Ensures both sides confirm the closure before releasing resources.

### Notes
- TCP Advantages: Reliable, ordered delivery, prevents flooding.
- TCP Disadvantages: Slower than UDP, needs a stable connection.
- Flags in handshake: SYN, ACK, SYN/ACK, FIN, RST.
- TCP is fun but heavier → used where reliability matters (web, email, file transfers).
- UDP is lighter/faster → used for streaming/gaming.


## Handshake Practical
- In this lab, I practiced the TCP handshake and connection,termination with a friend. We acted as client and server, exchanging messages step by step. It was interactive and fun, making the concept easier to remember.

**Steps followed:**
- SYN – Client: “Hey, can we talk?”
- SYN/ACK – Server: “Sure! Let’s sync up.”
- ACK – Client: “All set, let’s start.”
- DATA – Client: “Here’s my message.”
- ACK – Server: “Got your message!”
- FIN – Client: “I’m done talking. Let’s close this.”
- FIN/ACK – Server: “Closing too, acknowledged.”
- ACK – Client: “All closed. Goodbye!”



## UDP/IP

### Concepts Learned
- UDP is a stateless protocol, unlike TCP.
- No connection setup (no three-way handshake) or acknowledgements are required.
- Used when speed matters more than reliability (video streaming, voice chat, gaming).
- Packets may be lost, duplicated, or arrive out of order.
- UDP packets have simpler headers than TCP packets.

### Explanation
- Stateless Communication: Data is sent without establishing a connection.
- Fast Transmission: Less overhead than TCP because no handshake or continuous connection is required.
- Use Cases: Real-time applications where minor data loss is acceptable
- Packet Structure: Shares some headers with TCP (TTL, Source/Destination IP, Source/Destination Port, Data).
- Reliability Tradeoff: No built-in error-checking or sequencing – the application must handle any errors.

**Example Exchange (Alice ↔ Bob)**
- Alice: “Here’s my message.”
- -Bob: “Received message (maybe, if it arrived).”
- Alice: “Sending next message.”
- *Note: Unlike TCP, there are no SYN/ACK messages – packets are just sent and may arrive out of order.*

### Notes
- Advantages: Fast, no reserved connection, flexible for application flow control.
- Disadvantages: Unreliable, packets may be lost, no ordering or integrity guarantees.
- UDP Packets Include Headers: TTL, Source/Destination IP, Source/Destination Port, Data.
- Ideal for real-time or broadcast applications, where speed is prioritized over reliability.
  

## Ports

### Concepts Learned
- Ports are numerical endpoints (0–65535) where data is sent or received.
- Each port is associated with specific applications or protocols.
- Ports help enforce rules for communication between devices, ensuring correct data delivery.
- Common ports (0–1024) are reserved for widely-used protocols like HTTP, FTP, SSH.
- Applications can run on non-standard ports, but users must specify the port explicitly.

### Explanation
- Port Analogy: Like ships docking at a harbor; only compatible ships can dock at specific ports.
- Port Numbers: Range from 0 to 65535; standardized ports prevent confusion in busy networks.
- Standard Protocol Ports: FTP,SSH,HTTP,HTTPS,SMB,RD
- Non-Standard Ports: Applications can run on other ports (e.g., web server on 8080 instead of 80), but must specify the port when connecting.
- Ports allow multiple applications to communicate on the same device without conflicts.

### Notes
- Purpose: Directs data to the correct application on a device.
- Common Ports: 0–1024 are “well-known” or standard ports; others are ephemeral or custom.
- Protocols & Ports

## Practical Lab
- Task: Connect to IP 8.8.8.8 on port 1234 using the terminal interface.
- Method: Typed the command in a GUI-like search bar; the input was executed in the terminal automatically.
- Outcome: Successfully connected and received a flag.


