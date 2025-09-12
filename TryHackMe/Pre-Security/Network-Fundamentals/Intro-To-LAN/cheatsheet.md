# Cheatsheet - Intro To LAN

| Topic / Tool              | Description                                                                 | Example / Notes                                                      |
|---------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------|
| **LAN (Local Area Network)** | A network that connects devices within a limited area like home, office, or school | High speed, low latency; uses Ethernet/Wi-Fi                         |
| **Network Topologies**    | Structure of how devices are connected in a LAN                             | Star (common), Bus, Ring, Mesh; each has pros/cons                   |
| **Switch**                | Operates at Data Link Layer; forwards frames within LAN using MAC addresses | Central device connecting PCs, printers, servers                     |
| **Router**                | Connects different networks; routes data packets based on IP addresses      | Connects LAN to WAN/Internet                                         |
| **Subnetting**            | Splits a large network into smaller, logical sub-networks                   | Example: Employees subnet vs Guest subnet                            |
| **Subnet Mask**           | Defines which part of IP = network & which part = host                      | `255.255.255.0` → 24-bit network, 254 usable hosts                   |
| **ARP (Address Resolution Protocol)** | Resolves IP addresses to MAC addresses for local communication        | `arp -a` → shows ARP cache                                           |
| **DHCP (Dynamic Host Configuration Protocol)** | Automatically assigns IPs, subnet masks, gateway, DNS to devices      | Process: Discover → Offer → Request → Acknowledge (DORA)             |
| **Default Gateway**       | Device (usually router) that forwards traffic outside local subnet          | Commonly `.1` or `.254` in a subnet                                  |

