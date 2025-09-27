# Networking Essentials

## Introduction
- When a computer connects to a network, several background processes ensure that it can communicate properly. Network settings such as IP addresses, gateways, and DNS servers are often configured dynamically without user input. Devices also need a way to map IP addresses to physical hardware addresses, share a single public IP among many systems, and test connectivity across the internet.  
- This room introduces the key protocols and technologies that make this possible, including DHCP, ARP, NAT, ICMP, and tools like ping and traceroute. Together, these form the foundation that allows devices to interact seamlessly within local networks and across the internet.


## Dynamic Host Configuration Protocol (DHCP)

### Concepts Learned
- Dynamic Host Configuration Protocol (DHCP) automates the process of assigning IP addresses and network settings to devices, removing the need for manual configuration.

### Explanation
**When you connect a device to a new network, it needs three key settings:**
   - IP address + Subnet mask (to uniquely identify the device)
   - Default Gateway/Router (to communicate outside the local network)
**DNS server**
   - Manually configuring these works for servers (which should always keep the same IP), but it’s impractical for mobile or everyday devices.
   -  DHCP solves this by automatically assigning the right settings, preventing errors like IP conflicts.
**DHCP works at the application layer but uses UDP for communication:**
   - Server listens on UDP port 67
   - Client communicates from UDP port 68
**The protocol follows the DORA process:**
   - Discover – Client broadcasts a DHCPDISCOVER message searching for a server.
   - Offer – Server responds with a DHCPOFFER containing an available IP.
   - Request – Client replies with DHCPREQUEST to accept the offered IP.
   - Acknowledge – Server confirms with DHCPACK, completing the lease.
**At the end of this process, the client device is ready to use the network, having received:**
   - A leased IP address
   - The default gateway
   - A DNS server

### Notes
- DHCP prevents manual setup issues and avoids IP conflicts.
- Works by broadcasting to the network initially (client starts with 0.0.0.0 → 255.255.255.255).
- Critical for scalable networks with many dynamic devices.
- Servers and critical infrastructure often use static IPs instead of DHCP.


## Address Resolution Protocol (ARP)

### Concepts Learned
- Address Resolution Protocol (ARP) is used to map an IP address (Layer 3) to a MAC address (Layer 2), allowing proper delivery of packets within a local network (Ethernet or WiFi).

### Explanation
- When devices communicate on the same network, they send IP packets inside Ethernet (802.3) or WiFi (802.11) frames.
- An IP address identifies the host at Layer 3.
- A MAC address is needed at Layer 2 to deliver the frame.
**If Host A wants to talk to Host B on the same subnet, it must know Host B’s MAC address. Since devices don’t keep track of all MAC addresses all the time, ARP is used when needed:**
  - ARP Request – The source host broadcasts a message asking: “Who has IP X.X.X.X? Tell me.”
  - ARP Reply – The target host responds with its MAC address.
  - After this exchange, the two hosts can communicate directly using Ethernet/WiFi frames.

### Notes
- ARP messages are not encapsulated in IP or UDP packets; they are carried directly in Ethernet frames.
- The broadcast MAC address ff:ff:ff:ff:ff:ff is used for ARP Requests.
**Example:**
 - Host 192.168.66.89 → ARP Request for 192.168.66.1
 - Host 192.168.66.1 → ARP Reply with MAC 44:df:65:d8:fe:6c
 - ARP sits between Layer 2 and Layer 3:
 - Some argue it’s Layer 2 (deals with MAC).
 - Others say Layer 3 (supports IP operations).
 - The key takeaway: ARP bridges IP addresses to MAC addresses.


## Internet Control Message Protocol (ICMP)

### Concepts Learned
- ICMP is used for network diagnostics and error reporting (not for data transport).
- ping uses ICMP Echo Request/Reply to test reachability and measure round-trip time (RTT).
- traceroute (tracert on Windows) discovers the path to a host by exploiting TTL expiry and ICMP Time Exceeded messages.
- Firewalls or device policies can block ICMP or intermediate replies, affecting results.

### Explanation
- ICMP Echo: ping sends an Echo Request (Type 8); a reachable host responds with an Echo Reply (Type 0). Output shows replies, RTT per hop, packet loss, and summary statistics (min/avg/max/mdev).
- Traceroute mechanics: traceroute sends packets with increasing TTL (1, 2, 3…). Each router that decrements TTL to zero returns an ICMP Time Exceeded (Type 11) message, revealing that hop. When the packet reaches the destination, it typically responds (depending on protocol used by traceroute) and the trace completes.
- Why replies may be missing: routers or hosts may drop packets silently or block ICMP, show * * *, or return private addresses for internal hops. Results can vary between runs and by network policy.

### Notes
- Use ping -c <count> (Linux) to limit packets; results include packet loss and RTT stats.
- Windows command is tracert (syntax and behavior differ slightly from Linux traceroute).
- Interpreting traceroute: a hop showing a private IP usually indicates an internal/ISP hop; repeated * entries can indicate filtering.
- ICMP is invaluable for troubleshooting reachability and path issues but is not a definitive measure of overall service health (some services block ICMP while still working).
- Remember: ICMP is a control/diagnostic protocol — treat its responses as hints, not guarantees.


## Routing

### Concepts Learned
- Routing decides how data packets travel between networks.
- Routers use routing tables to select the best path.
- Multiple routes may exist, so routing protocols define how to choose the most efficient one.

### Explanation
**Routing ensures packets can move beyond the local network and reach distant destinations. Each router makes forwarding decisions based on its routing table. To keep routes updated and efficient, different protocols are used:**
  - OSPF (Open Shortest Path First): Link-state protocol where routers share link information to build a complete network map and calculate shortest paths.
  - EIGRP (Enhanced Interior Gateway Routing Protocol): Cisco proprietary, combines link-state and distance-vector features, and uses metrics like bandwidth and delay.
  - BGP (Border Gateway Protocol): The backbone protocol of the Internet, used between ISPs and organizations to exchange routing info across Autonomous Systems.
  - RIP (Routing Information Protocol): Simple distance-vector protocol, selects routes based on hop count. Works for small networks but not scalable.

### Notes
**Routing protocols are divided into two main types:**
- IGPs (Interior Gateway Protocols): OSPF, EIGRP, RIP – operate inside an organization.
- EGPs (Exterior Gateway Protocols): BGP – operates between organizations.
- Efficient routing prevents loops, reduces delay, and ensures scalability across networks.


## Network Address Translation (NAT)

### Concepts Learned
- IPv4 has a limited address space (~4.3 billion addresses). NAT helps overcome this limitation.
- NAT allows multiple private devices to share a single public IP for Internet access.
- Routers with NAT maintain a translation table mapping internal (private) addresses/ports to external (public) ones.

### Explanation
- NAT extends the usability of IPv4 by letting many devices in a private network connect to the Internet using one public IP address. When a device (e.g., a laptop) initiates a connection, the NAT router rewrites the private source IP and port with its own public IP and a new port number.
**For example:**
  - Internal: 192.168.0.129:15401 → NAT router
  - External (translated): 212.3.4.5:19273 → Web server
- The web server only sees the public IP (212.3.4.5), while the router keeps track of the mapping to deliver responses back to the right internal device.

### Notes
**Types of NAT:**
  - SNAT (Static NAT): One private IP mapped to one public IP.
  - DNAT (Dynamic NAT): Multiple private IPs mapped dynamically to available public IPs.
  - PAT (Port Address Translation / NAT Overload): Many private IPs share one public IP using different port numbers (most common).
  - NAT conserves IPv4 addresses and adds a layer of security by hiding internal IPs.
- However, it can break some protocols that embed IP addresses in packet payloads (e.g., VoIP, gaming).


## Key Takeaways
- DHCP: Automates IP configuration (IP, subnet mask, gateway, DNS) using the DORA process (Discover, Offer, Request, Acknowledge), preventing address conflicts.
- ARP: Resolves IP addresses to MAC addresses on the local network, enabling devices to communicate at the data link layer.
- ICMP: Used for network diagnostics and error reporting. ping checks connectivity, and traceroute maps the route packets take across networks.
- Routing: Routers determine the best paths for packet delivery using protocols like OSPF, EIGRP, BGP, and RIP.
- NAT: Conserves IPv4 addresses by translating multiple private addresses to a single public IP, allowing multiple devices to access the Internet through one public IP.
