# Cheatsheet - Tcpdump Basics

## Basic Commands
| Command | Explanation |
|---------|-------------|
| `tcpdump -i INTERFACE` | Capture packets on a specific network interface |
| `tcpdump -w FILE.pcap` | Write captured packets to a file |
| `tcpdump -r FILE.pcap` | Read packets from a capture file |
| `tcpdump -c NUM` | Limit capture to a specific number of packets |
| `tcpdump -n` | Don’t resolve hostnames (faster, raw IPs) |

## Filtering Expressions
| Command | Explanation |
|---------|-------------|
| `tcpdump host IP` | Capture packets to/from a specific host |
| `tcpdump src host IP` | Capture packets from a specific source host |
| `tcpdump dst host IP` | Capture packets to a specific destination host |
| `tcpdump port PORT` | Capture traffic on a specific port |
| `tcpdump src port PORT` | Capture packets from a specific source port |
| `tcpdump dst port PORT` | Capture packets to a specific destination port |
| `tcpdump PROTOCOL` | Filter by protocol (e.g., tcp, udp, icmp, ip, ip6) |
| `and`, `or`, `not` | Combine filters with logical operators |

## Advanced Filtering
| Command | Explanation |
|---------|-------------|
| `greater LENGTH` | Capture packets larger than or equal to a specific length |
| `less LENGTH` | Capture packets smaller than or equal to a specific length |
| `proto[expr:size]` | Filter by contents of protocol header bytes |
| `tcpdump "tcp[tcpflags] == tcp-syn"` | Capture packets with only the SYN flag set |
| `tcpdump "tcp[tcpflags] & tcp-ack != 0"` | Capture packets with the ACK flag set |
| `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"` | Capture packets with SYN or ACK flags |

## Displaying Packets
| Command | Explanation |
|---------|-------------|
| `tcpdump -q` | Quick/brief output |
| `tcpdump -e` | Include MAC addresses (link-layer info) |
| `tcpdump -A` | Display packet contents in ASCII |
| `tcpdump -xx` | Display packet data in hex |
| `tcpdump -X` | Display packet data in both hex and ASCII |
