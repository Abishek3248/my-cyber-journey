# Networking Concepts

## Introduction
- Networking forms the backbone of communication between devices, systems, and applications.
- Understanding data flow, device communication, and governing protocols is essential for cybersecurity and IT.
- The ISO OSI model provides a conceptual framework with seven layers, helping visualize how data moves from one device to another.
- The TCP/IP protocol suite is a practical set of protocols that enable real-world network communication, forming the foundation of the internet and local networks.
- Together, these models help analyze, troubleshoot, and secure networks effectively.


## OSI Model

### Concepts Learned
- ISO OSI model is a conceptual framework standardizing how network communication occurs.
- It has 7 layers, each with distinct responsibilities: Physical, Data Link, Network, Transport, Session, Presentation, and Application.
- Understanding OSI layers aids in networking, troubleshooting, and interpreting network devices/protocols.
- Key protocols and functions map to specific layers (e.g., TCP at Transport, HTTP at Application).

### Explanation
- Physical Layer (Layer 1): Transmits raw data using physical media like cables, optical fiber, or wireless signals.
- Data Link Layer (Layer 2): Ensures reliable communication within a network segment using MAC addresses (e.g., Ethernet, WiFi).
- Network Layer (Layer 3): Handles logical addressing and routing between networks (e.g., IP, ICMP, VPN).
- Transport Layer (Layer 4): Provides end-to-end communication, flow control, segmentation, and error checking (TCP/UDP).
- Session Layer (Layer 5): Establishes, maintains, and synchronizes communication sessions between applications (e.g., RPC, NFS).
- Presentation Layer (Layer 6): Formats, encodes, compresses, and encrypts data for applications (e.g., ASCII, Unicode, JPEG, MIME).
- Application Layer (Layer 7): Provides network services directly to end-user applications (e.g., HTTP, FTP, DNS, SMTP, IMAP).

### Notes
- Layer numbers are important; they are referenced in terms like Layer 3 switch or Layer 7 firewall.
- Each layer only interacts with adjacent layers but works together for end-to-end communication.
- OSI model is theoretical but essential for understanding networking protocols and network troubleshooting.


## TCP/IP Model

### Concepts Learned
- TCP/IP (Transmission Control Protocol/Internet Protocol) is a practical, implemented model for network communication.
- Developed by the US Department of Defense (DoD) in the 1970s, it ensures network resilience even if parts fail.
- TCP/IP layers map closely to OSI layers but are grouped differently for practical implementation.
- Protocols like TCP, UDP, IP, HTTP, and FTP operate within specific TCP/IP layers.

### Explanation
- Application Layer: Combines OSI layers 5–7 (Application, Presentation, Session) and provides services to end-user applications (HTTP, FTP, SSH, SMTP).
- Transport Layer: Corresponds to OSI Layer 4, responsible for end-to-end communication, segmentation, and error handling (TCP, UDP).
- Internet Layer: Maps to OSI Layer 3; handles logical addressing and routing between networks (IP, ICMP, IPSec).
- Link Layer: Combines OSI Layers 1–2; responsible for physical transmission and data link protocols (Ethernet 802.3, WiFi 802.11).

### Notes
- Some textbooks represent TCP/IP as a 5-layer model, including the Physical layer separately.
- Understanding the TCP/IP model helps in configuring networks, troubleshooting, and analyzing protocol behavior.
- TCP/IP is the foundation of the modern Internet, making it essential for cybersecurity and networking studies.


## IP Addresses and Subnets

### Concepts Learned
- IP addresses are unique identifiers assigned to devices on a network.
- IPv4 is the most common version, consisting of 32 bits divided into four octets.
- IP addresses include network, host, and broadcast addresses.
- Subnetting defines the portion of an IP address that identifies the network and the portion that identifies the host.
- Private and public IP addresses serve different purposes: private addresses are isolated from the Internet, while public addresses are globally routable.
- Routers forward packets between networks based on IP addresses.

### Explanation
- IP Address Structure: Four octets (0–255) representing 32 bits. Example: 192.168.66.89.
- Network & Broadcast: .0 denotes the network, .255 denotes the broadcast address in a /24 subnet.
- Subnet Masks: Define network and host bits. /24 = first 24 bits are network bits; addresses range from .1 to .254.
**Private IP Ranges (RFC 1918):**
  - 10.0.0.0 – 10.255.255.255
  - 172.16.0.0 – 172.31.255.255
  - 192.168.0.0 – 192.168.255.255
- Routing: Routers forward packets between networks using the destination IP address.

### Notes
- Commands to check IP configuration:
- Linux: ifconfig or ip a s
- Windows: ipconfig
- Understanding subnetting and IP addressing is crucial for network configuration, troubleshooting, and cybersecurity practices.
- Memorize private IP ranges for easier recognition of internal vs external addresses.


## UDP and TCP

### Concepts Learned
- Transport layer protocols (Layer 4) enable communication between processes on networked hosts.
- UDP is connectionless and does not guarantee delivery.
- TCP is connection-oriented and ensures reliable delivery using acknowledgments and sequence numbers.
- Port numbers identify specific processes on a host; valid range is 1–65535, with 0 reserved.
- TCP uses a three-way handshake (SYN, SYN-ACK, ACK) to establish a connection.

### Explanation
**UDP (User Datagram Protocol):**
  - Sends packets without establishing a connection.
  - No delivery confirmation; faster and simpler.
  - Similar to standard mail with no delivery receipt.
**TCP (Transmission Control Protocol):**
  - Establishes a connection before sending data.
  - Uses sequence and acknowledgment numbers for reliability.
  - Ensures packets are received in order and retransmits lost packets.
**Connection setup via three-way handshake:**
  - SYN: Client initiates connection.
  - SYN-ACK: Server responds.
  - ACK: Client confirms connection.

### Notes
- UDP is suitable for speed-critical applications (e.g., streaming, DNS queries).
- TCP is used for applications requiring reliability (e.g., HTTP, FTP, email).
- Understanding TCP vs UDP is essential for network configuration, troubleshooting, and security monitoring.


## Encapsulation

### Concepts Learned
- Encapsulation is the process of each layer adding a header (and sometimes a trailer) to the data from the layer above.
- Allows layers to focus on their specific functions while passing data down the stack.
- Reversed on the receiving end to extract the original application data.

### Explanation
- Application Layer: User creates data (e.g., email, message) which is passed to the transport layer.
- Transport Layer: Adds TCP or UDP headers, forming a segment or datagram.
- Network Layer: Adds IP headers, creating an IP packet for routing.
- Data Link Layer: Adds link layer headers and trailers, forming frames (Ethernet/WiFi) for physical transmission.
- On the receiving end, each layer strips its header/trailer until the original data reaches the application.

### Notes
- Encapsulation ensures modularity and separation of responsibilities across layers.
- A packet travels through encapsulation at the sender and decapsulation at the receiver.
- Example: Searching on a web page involves the HTTP request encapsulated in TCP, then IP, then Ethernet/WiFi frame, routed through multiple devices until reaching the server.


## Telnet

### Concepts Learned
- Telnet is a simple TCP-based protocol and client used for establishing remote text/terminal connections to a service listening on a TCP port.
- It can speak plain-text protocols (echo, daytime, HTTP) by opening a raw TCP connection and sending text.
- Telnet is insecure for remote administration because it sends data (including credentials) in cleartext — prefer SSH for interactive shells.

### Explanation
- Basic usage: telnet <host> <port> — opens a TCP connection to the given host and port.
**Common demo services:**
  - Echo (port 7): echoes back whatever you send.
  - Daytime (port 13): returns the current date/time and then closes the connection.
  - HTTP (port 80): you can issue a raw HTTP request, e.g.:
     **GET / HTTP/1.1
     Host: example.com**
- Interactive controls: Ctrl + ] enters the telnet client prompt (on many clients) where you can type quit to close the session.

### Notes
- Telnet is useful for quickly testing TCP services, verifying banners, and manually crafting simple protocol exchanges.
- Typical troubleshooting uses: check if a port is reachable, view service banners, or test simple protocol responses.
- Security: never use telnet for remote login on production systems — credentials and session data are unencrypted. Use SSH for secure remote shells.
- When testing HTTP with telnet, the server’s response often includes the server banner/version in the Server: header — useful for service identification (but may be omitted or masked by operators).
- If a telnet connection closes immediately (e.g., daytime service), that behavior can be normal for that service.
**Example quick checks:**
  - telnet 10.10.10.5 7 → echo server interaction.
  - telnet 10.10.10.5 13 → daytime server returns time then disconnects.
  - telnet 10.10.10.5 80 → send GET / HTTP/1.1 + Host: header + blank line to fetch HTTP response.
 

## Key Takeaways
- The ISO OSI and TCP/IP models provide conceptual and practical frameworks for understanding how network communication occurs across layers.
- IP addresses uniquely identify devices on a network, while subnets organize networks and help route traffic efficiently. Private and public IP ranges serve different purposes.
- TCP and UDP are transport-layer protocols: TCP ensures reliable, connection-oriented communication with sequencing and acknowledgements, whereas UDP is connectionless and faster but unreliable.
- Encapsulation allows each layer to add headers (and sometimes trailers) to data, enabling modular functionality and proper communication from applications to physical transmission.
- Routers operate at layer 3 to forward packets between networks, ensuring data reaches its destination efficiently.
- Telnet demonstrates how clients can manually interact with network services on specific ports, highlighting request-response communication patterns and the concept of service ports.
- Overall, these concepts establish a strong foundation for understanding how data travels across networks, how hosts and services communicate, and how protocols and addressing work together in real-world networking scenarios.
