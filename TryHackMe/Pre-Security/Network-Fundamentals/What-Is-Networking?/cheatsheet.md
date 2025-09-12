# Cheatsheet - what is networking


| Topic / Tool           | Description                                                                                  | Example / Notes                                                      |
|------------------------|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| **IP Address**          | Unique identifier for a device on a network; can be public or private                        | `192.168.1.77` (private), `86.157.52.21` (public)                   |
| **MAC Address**         | Hardware-based identifier for a network interface; can be spoofed                             | `a4:c3:f0:85:ac:2d` — first 6 hex = vendor, last 6 hex = unique     |
| **Ping (ICMP Echo)**    | Test if a device is reachable on a network; measures latency and packet loss                 | `ping 192.168.1.1`                                                   |
| **Traceroute**          | Maps the route packets take to a destination; identifies intermediate network hops           | `traceroute example.com`                                             |
| **ARP / Device Mapping**| Resolves IP addresses to MAC addresses on local network                                       | `arp -a`                                                              |
| **Network Layer Concepts** | Understanding of Layer 3, private vs public networks, IPv4 vs IPv6                            | IPv4 = 4.29B addresses, IPv6 = 340T+ addresses                       |
| **ICMP Messages**       | Types include Echo Request/Reply, Destination Unreachable, Time Exceeded                     | Useful for diagnosing connectivity issues                             |

