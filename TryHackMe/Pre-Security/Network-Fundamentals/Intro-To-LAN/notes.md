# Intro to LAN (Local Area Network)

## Introduction
A Local Area Network (LAN) is a network that connects devices within a limited geographic area such as a home, office, or school. LANs enable fast communication and resource sharing (like files, printers, or internet access) between computers and other devices. They typically use Ethernet cables or Wi-Fi, and because of their limited scope, LANs offer high speed, low latency, and strong control compared to larger networks like WANs.


## Introducing LAN Topologies

### Concepts Learned
- Role of switches (connecting devices within the same network) and routers (connecting multiple networks and directing traffic).
- Different LAN topologies: Bus, Star, Ring, Mesh, each with unique strengths and weaknesses.
- How failures in each topology affect overall connectivity and reliability.

### Explanation
- LAN topologies determine how devices are arranged and interconnected within a network.
- Bus topology is simple but a single cable failure can take down the entire network.
- Star topology connects all devices to a central switch or hub, making it easy to manage but dependent on that central device.
- Ring topology connects devices in a loop where data flows in one direction, but one failure can disrupt the whole chain.
- Mesh topology provides high redundancy by interconnecting devices with multiple links, improving fault tolerance but adding cost and complexity.
- *Through lab simulations, I was able to visualize these topologies in action—understanding not just their design but also how each one fails and recovers. This highlighted why topology choice is crucial for balancing performance, reliability, and cost.*

### Notes
- Switches operate at Layer 2 (Data Link), managing traffic within a LAN.
- Routers operate at Layer 3 (Network), connecting multiple networks (LANs to WANs, or LAN to Internet).
- Topology choice influences scalability, fault tolerance, and maintenance complexity.
- Practical takeaway: Star topologies are widely used in modern LANs due to simplicity and scalability, while mesh is reserved for high-reliability environments.


## Introduction to Subnetting and Network Segmentation

### Concepts Learned
- Subnetting is the process of dividing a larger network into smaller, manageable sub-networks.
- Subnet masks determine how IP addresses are split into network, host, and gateway parts.
- Subnetting supports efficiency, security, and administrative control in both small and enterprise networks.
- Practical use cases include separating employee networks from public Wi-Fi in cafés or segregating business departments.

### Explanation
- Subnetting is like slicing a cake — the whole cake (network) is finite, but subnetting divides it into smaller slices (subnets), ensuring fair and efficient use. Each subnet has:
- Network Address → identifies the subnet itself.
- Host Address → identifies devices (PCs, printers, IoT) within that subnet.
- Default Gateway → the device that connects the subnet to other networks, usually assigned .1 or .254.
- In small home networks, one subnet is usually enough (e.g., up to 254 devices). In larger environments like offices, subnetting separates departments or use cases to reduce congestion, improve security, and allow more precise management.

### Notes
- Learned that private networks often use subnetting to separate traffic types (e.g., staff vs. public users).
- Understood how subnetting helps isolate sensitive resources while maintaining connectivity.
- Practical takeaway: subnetting isn’t just about saving addresses; it’s a security and organizational strategy for modern networks.


## ARP (Address Resolution Protocol)

### Concepts Learned
- Devices on a network have two identifiers: IP address (logical) and MAC address (physical).
- ARP (Address Resolution Protocol) is used to map an IP address to its corresponding MAC address.
- Each device keeps a record of known IP-to-MAC mappings in an ARP cache.
- Communication happens through two key message types:
- ARP Request – a broadcast asking “Who owns this IP address?”
- ARP Reply – the device with that IP responds with its MAC address.

### Explanation
- When a device wants to communicate with another device on the same network, it needs the destination’s MAC address. Since devices typically know the IP address but not the MAC, they use ARP to resolve this.
- The requesting device sends an ARP Request (broadcast) to the entire network.
- The device that owns the IP address replies with an ARP Reply, providing its MAC address.
- The requesting device then stores this mapping (IP ↔ MAC) in its ARP cache for faster communication in the future.
- This allows devices to find each other on the local network and communicate efficiently without repeatedly broadcasting requests.

### Notes
- ARP Cache: Temporary storage for known IP-to-MAC mappings. Speeds up communication.
- Efficiency: Reduces repeated broadcasts by storing mappings.
- Security: Vulnerable to ARP spoofing/poisoning, where attackers send false ARP replies to mislead devices.
- Practical use: Useful in troubleshooting and understanding how packets reach the correct device.


## Dynamic Host Configuration Protocol (DHCP)

### Concepts Learned
- DHCP (Dynamic Host Configuration Protocol) automates the assignment of IP addresses to devices on a network.
- It prevents manual configuration errors and ensures efficient IP address management.
- Follows a four-step process: Discover → Offer → Request → Acknowledge.

### Explanation

- When a device joins a network without a pre-assigned IP, it broadcasts a DHCP Discover to locate a DHCP server.
- The server responds with a DHCP Offer, suggesting an available IP address.
- The device confirms by sending a DHCP Request, and finally, the server replies with a DHCP Acknowledgment (ACK), completing the process.
- This protocol is widely used in home, office, and enterprise networks, as it simplifies network administration by dynamically allocating IP addresses, subnet masks, gateways, and DNS settings.

### Notes
- DHCP uses UDP ports 67 (server) and 68 (client).
- It reduces the risk of IP conflicts compared to manual assignments.
- In enterprise setups, DHCP can be combined with reservations to ensure critical devices (e.g., servers, printers) always receive the same IP
- Security concern: Rogue DHCP servers can mislead clients and redirect traffic (used in attacks like MITM).


## Key Takeaways
- LANs provide fast, reliable communication within a limited area and form the foundation of modern networking.
- Different topologies (bus, star, ring, mesh) define how devices interconnect, each with unique strengths and weaknesses.
- Switches and routers are essential LAN devices: switches connect devices within the same network, while routers connect different networks.
- Subnetting allows efficient IP address allocation, improves security, and helps isolate departments or use cases.
- ARP maps IP addresses to MAC addresses, enabling devices to locate and communicate with each other.
- DHCP simpifies IP management by automatically assigning addresses, reducing conflicts, and ensuring smooth device onboarding.
