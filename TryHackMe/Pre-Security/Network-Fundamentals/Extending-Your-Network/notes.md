# Extending Your Networking

## Introduction to Port Forwarding

### Concepts Learned
- What port forwarding is and why it’s important.
- Difference between intranet-only access and making services publicly accessible.
- How routers handle port forwarding.
- Difference between port forwarding and firewalls.

### Explanation
- Port forwarding allows devices and services inside a private LAN (like a web server on 192.168.1.10:80) to be accessible from the outside world (Internet). Without it, services remain available only inside the LAN (intranet).
- By configuring port forwarding on a router, incoming traffic to a public IP address (e.g., 82.62.51.70) can be directed to a private IP inside the LAN.
- Intranet scenario: only internal devices (same network) can access the web server.
- Port forwarding scenario: external devices (Internet) can access the service through the router’s public IP.
- It’s important to note the distinction:
- Port Forwarding = opens a specific port for access.
- Firewall = controls whether or not traffic is allowed through those ports.
- Port forwarding is always configured on the router, which acts as the gateway between private and public networks.

### Notes
- Port forwarding makes internal services public (can be risky if misconfigured).
- Router level configuration ensures traffic on specific ports is forwarded to the right internal device.
- Common use cases: web servers (port 80/443), gaming servers, remote desktop (3389), FTP servers (21).
- Firewalls and port forwarding work together:
- Forwarding opens the door.
- Firewall decides who can enter.



## Firewall

### Concepts Learned
- Purpose of a firewall in controlling network traffic.
- Factors firewalls consider: source, destination, port, and protocol.
- The difference between stateful and stateless firewalls.
- Real-world use of hardware, software, and built-in router firewalls.

### Explanation
- A firewall acts as border security for a network, deciding what traffic can enter or exit. It inspects packets and makes decisions based on:
- Source: where the traffic is coming from.
- Destination: where the traffic is going.
- Port: which service or application the traffic is for.
- Protocol: whether it’s TCP, UDP, or another protocol.
 **Firewalls can be:**
- Hardware-based (enterprise-level, high performance).
- Software-based (like Snort).
- Built into home routers (basic protection).
- Firewalls perform packet inspection and can operate as either:
 **Stateful Firewall**
- Monitors entire connection sessions, not just single packets.
- Dynamic — decisions are based on full connection behavior.
- Blocks entire devices if suspicious activity is detected.
- Pros: Smart, adaptive, secure.
- ons: Resource heavy, can slow performance.
 **Stateless Firewall**
- Uses predefined static rules for individual packets.
- Lightweight — good against large traffic floods (like DDoS).
- Pros: Fast, low resource usage.
- Cons: Limited intelligence, only as good as its rule set.

### Notes
- Stateful = smart but resource intensive
- Stateless = fast but less flexible.
- Firewalls are everywhere: enterprise hardware, home routers, and software-based solutions.
- Firewalls + Port Forwarding work together → forwarding opens the door, firewall decides who gets through.


## Firewall Practical (Blocking Malicious Packets)

### Concepts Learned
- How to identify malicious vs legitimate traffic in a network environment.
- The role of firewalls in filtering traffic based on IPs, ports, and protocols.
- Practical application of firewall rules using the DROP action to block traffic silently.

### Explanation
- In this task, an interactive lab simulated a scenario where malicious packets (red) were targeting a web server (203.0.110.1) over port 80 (HTTP). The objective was to block these malicious packets while still allowing legitimate traffic (green) to pass.
- To achieve this, firewall rules were configured to:
- Inspect source and destination IPs.
- Target port 80 traffic.
- Apply the DROP action, ensuring malicious traffic was silently discarded without alerting the attacker.
- This demonstrated how firewalls can protect critical services by filtering based on conditions such as source IP, destination IP, and port numbers.

### Notes
- Malicious traffic = red packets; Legitimate traffic = green packets.
- Target web server IP: 203.0.110.1.
 **Firewall rule specifics:**
- Source IP: malicious client’s IP
- Destination IP: 203.0.110.1
- Port: 80 (HTTP)
- Action: DROP
- Result: Malicious packets blocked, legitimate packets passed successfully.

## VPN Basics

### Concepts Learned
- What a VPN is and how it works.
- Benefits of VPNs (privacy, anonymity, connecting networks).
- How TryHackMe uses VPNs.
- Different VPN technologies: PPP, PPTP, IPSec.

### Explanation
- A VPN (Virtual Private Network) creates an encrypted tunnel between devices across different networks, allowing them to securely communicate as if they were in the same private network.
- Example: Two offices in separate locations can securely share resources through a VPN tunnel.
**Benefits of VPNs:**
- Connects networks across locations → Businesses can link multiple offices.
- Privacy → Encryption prevents sniffing (especially on public WiFi).
- Anonymity → ISPs and intermediaries cannot easily track traffic; activists/journalists use this in restrictive environments.
**VPN at TryHackMe:**
- Ensures secure connections to vulnerable machines.
- Prevents ISPs from flagging activity as malicious.
- Protects vulnerable machines from direct Internet exposure.
**VPN Technologies:**
- PPP (Point-to-Point Protocol): Handles authentication and encryption, but non-routable.
- PPTP (Point-to-Point Tunneling Protocol): Lets PPP traffic leave the network, easy to set up but weak encryption.
- IPSec (Internet Protocol Security): Strong encryption using IP framework, more complex setup but widely supported.

### Notes
- VPNs form a secure private network (tunnel) over the Internet.
- Provide privacy (encryption), anonymity (masking traffic), and connectivity (linking networks).
- Security depends on VPN provider’s policies (e.g., logging).
- TryHackMe VPN example: safe, controlled access to labs without exposure.


## LAN Devices

### Concepts Learned
- Role of a Router in connecting networks and determining data paths.
- Role of a Switch in connecting multiple devices and forwarding traffic.
- Differences between Layer 2 and Layer 3 switches.
- Introduction to VLANs for logical network segmentation and security.

### Explanation
**Router**
- Connects different networks and forwards data between them using routing protocols.
- Operates at Layer 3 (Network layer) of the OSI model.
- Administrators can configure port forwarding, firewall rules, and routing policies through an interface.
 *Routing decisions depend on:*
- Shortest path
- Most reliable path
- Fastest medium (e.g., copper vs fiber)
- Example: Computer A can reach Computer B through multiple routers. The router decides the best path based on the protocol in use.
**Switch (Layer 2)**
- Dedicated device that connects multiple devices in a LAN using Ethernet cables.
- Operates at Layer 2 (Data Link layer).
- Uses MAC addresses to forward frames to the correct device.
- Does not handle routing across different networks.
**Switch (Layer 3)**
- More advanced; combines functions of a switch and some features of a router.
- Can forward frames (like Layer 2) and route packets using IP addresses.
*Supports VLANs (Virtual LANs):*
- Logical separation of devices within the same network.
- Increases security by restricting communication between groups.
- Example: Sales and Accounting departments can both access the Internet but cannot communicate with each other directly.

### Notes
- Router = Connects different networks and finds the best path.
- Switch (Layer 2) = Connects devices in the same network using MAC addresses.
- Switch (Layer 3) = Combines switch + router features, supports VLANs.
- VLAN = Logical network segmentation for security and organization.



## Practical Network Simulator — TCP Packet Lab

### Concepts Learned
- The TCP three-way handshake (SYN → SYN-ACK → ACK) and how it establishes a reliable connection before data transfer.
- How ARP resolves IP → MAC on the local link so frames can be delivered.
- The step-by-step packet flow across devices (how a packet moves from host → switch → router → destination).
- Using a simulator to visualize protocol interactions and confirm successful delivery (and capture the flag).

### Explanation
- The simulator let me watch every stage a TCP packet takes from Computer1 to Computer3. Before any TCP packets can be delivered on the local network, the sender checks its ARP cache; if the destination MAC is unknown, it broadcasts an ARP Request and receives an ARP Reply with the target’s MAC. With the MAC known, the sender begins the TCP connection process: it sends a SYN, the receiver replies SYN-ACK, and the sender completes the handshake with an ACK — only then is the actual TCP payload transmitted. Observing this visually clarified how link-layer (ARP), network-layer (IP), and transport-layer (TCP) activities interlock.

### Notes
- I deployed the static site and used the simulator to send a TCP packet from Computer1 → Computer3; completing the handshake and subsequent data transfer revealed the lab flag.
- The visual step-through made it easy to see where packets were dropped or delayed and how ARP cache entries speed up subsequent transmissions.
- This lab reinforced how critical proper name/address resolution (ARP) and reliable connection setup (TCP) are in real networks — both for normal operations and when troubleshooting or performing network assessments.


## Key Takeaways
- Understood Port Forwarding and how it exposes internal services (like a web server) to external networks.
- Learned the role of Firewalls in filtering traffic based on rules (source, destination, ports, protocols) and the difference between stateful and stateless firewalls.
- Practiced configuring firewall rules to block malicious traffic targeting specific ports and IPs.
- Explored VPN basics, including tunneling, encryption, anonymity, and how VPNs connect networks across geographic locations.
- Learned about VPN technologies (PPP, PPTP, IPSec) and their strengths/weaknesses.
- Gained insights into LAN devices like routers and switches, their OSI layers, and VLANs for segmentation and security.
- Used a network simulator to visualize ARP resolution, TCP handshakes, and packet transmission end-to-end, reinforcing how protocols interoperate.

