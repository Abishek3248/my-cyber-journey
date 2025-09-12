# What is Networking?

## Introduction
- Networking is the practice of connecting devices to share information and resources, much like people connect through friendships or cities through transport systems. In computing, networks can range from two devices to billions, including phones, laptops, cameras, and even critical infrastructure. Because modern life—from electricity to communication—depends on them, understanding networking is a core foundation for both technology and cybersecurity.


## Internet
### Concepts Learned
- The Internet is essentially a giant network of interconnected smaller networks.
- Networks are categorized as private networks (internal, restricted) or public networks (the Internet itself).
- The Internet’s origins trace back to ARPANET (1960s), with the modern web built on Tim Berners-Lee’s World Wide Web (1989).

### Applied Networking Concepts
- Think of the Internet as multiple smaller networks (friends) being linked together through intermediaries (like Alice acting as a messenger).
- This interconnected system allows global communication, resource sharing, and scalability far beyond a single network.
- Networking concepts such as addressing and labels are crucial to ensure devices can identify and communicate across private and public networks.

### Notes
- The Internet is the largest network of networks, combining both private and public connections. It began with ARPANET and evolved into the World Wide Web, becoming a universal platform for communication and information sharing.
- At its core, it relies on small, local networks linking into larger public ones, enabling billions of devices to interact.



## IP & MAC Addressing (Identifying Devices on a Network)

### Concepts Learned
- **IP Address** — a logical, routable identifier assigned to a device on a network (IPv4 / IPv6).  
- **Public vs Private IPs** — private IPs identify devices inside a local network; a single public IP identifies that network to the Internet (assigned by an ISP).  
- **IPv4 vs IPv6** — IPv4 uses 32-bit addressing (≈4.29 billion addresses); IPv6 uses 128-bit addressing to solve address exhaustion.  
- **MAC Address** — a permanent hardware identifier assigned to a network interface (12-hex chars, e.g. `a4:c3:f0:85:ac:2d`); first half = vendor, second half = unique NIC ID.  
- **MAC spoofing** — MACs can be forged to impersonate another device, bypassing simplistic MAC-based access controls.

### Applied Networking Concepts
- IP addresses are **logical** and can change (DHCP, reassignment); they are required for routing packets between networks.  
- MAC addresses are **physical/low-level identifiers** used on the local network segment for frame delivery; they do not get routed across the Internet.  
- Addressing schemes and protocols (IP, ARP, etc.) together allow devices to locate and communicate with each other across private and public networks.  
- MAC spoofing demonstrates a key security limitation: **trusting hardware identifiers alone is insecure**. Access controls should combine authentication, encryption, and monitoring rather than rely solely on MAC filtering.

### Notes
- Practically tested MAC spoofing in the lab: changing a device’s MAC allowed access to the network privileges originally granted to the legitimate device — a useful hands-on demonstration of how MAC-based restrictions can be bypassed.  
- Learned the difference between identifying a device at the link layer (MAC) vs. the network layer (IP), and why both matter for enumeration and exploitation during network assessments.  
- IPv6 was noted as the long-term solution to IPv4 exhaustion and introduces new operational considerations (addressing scale and different attack surface).  




## PING & ICMP

### Concepts Learned
- **ICMP (Internet Control Message Protocol)** — a core network protocol used for error reporting and diagnostics within IP networks.  
- **Ping utility** — sends ICMP Echo Request packets and expects Echo Reply packets to test device reachability.  
- **Traceroute** — leverages ICMP (or UDP/TCP variants) to map the path packets take across networks.  
- ICMP is integral for identifying **latency, packet loss, and routing issues**.  

### Applied Networking Concepts
- ICMP operates at the **Network Layer (Layer 3)** alongside IP, but is used for **control and troubleshooting** rather than application data transfer.  
- Security concern: ICMP can be abused for reconnaissance (e.g., host discovery, network mapping) and covert channels (ICMP tunneling).  
- In restricted environments, ICMP traffic may be blocked or rate-limited to mitigate scanning and DoS attacks.  
- Tools like **Ping and Traceroute** remain foundational in both system administration and penetration testing for assessing connectivity and diagnosing network issues.  

### Notes
- Practically observed that `ping` can quickly confirm whether a host is online, but does not guarantee service availability (host may block ICMP yet still serve traffic).  
- Understood how **ICMP echo, time-exceeded, and destination-unreachable messages** aid in pinpointing connectivity problems.  
- Key takeaway: ICMP is both a **vital troubleshooting protocol** and a **potential security risk**, depending on context.
- Hands-on practice: Successfully pinged a live website to observe response times and packet loss, reinforcing the role of ICMP in connectivity testing.



### Key Takeaway
- This module has provided a foundational understanding of networking concepts, including what networks and the Internet are, how devices are identified using IP and MAC addresses, the role of ICMP in connectivity testing, and practical tools like ping and traceroute.
- These fundamentals are essential for troubleshooting, ensuring reliable communication between devices, and building a strong base for cybersecurity and penetration testing.



