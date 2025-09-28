# Summary – Tcpdump Basics

This module strengthened my understanding of packet capturing, filtering, and analyzing network traffic using Tcpdump, providing practical skills to inspect network communications in real time or from capture files.

- Learned the importance of specifying the network interface to capture packets and how to list available interfaces using `ip a`.
- Understood how to save captured packets to a file (`-w FILE`) and read them later (`-r FILE`) for detailed analysis.
- Practiced limiting the number of captured packets (`-c COUNT`) and disabling DNS and port resolution (`-n` / `-nn`) to improve performance.
- Explored filtering expressions to focus on relevant traffic: by host (`host`, `src host`, `dst host`), by port (`port`, `src port`, `dst port`), by protocol (`tcp`, `udp`, `icmp`, `ip`, `ip6`), and using logical operators (`and`, `or`, `not`).
- Learned advanced filtering techniques including packet length filters (`greater`, `less`) and TCP flag filters (`tcp[tcpflags]`) to capture specific types of TCP packets like SYN, ACK, or combinations.
- Practiced displaying packets in various formats for analysis: brief output (`-q`), link-level headers (`-e`), ASCII (`-A`), hexadecimal (`-xx`), or both hex and ASCII (`-X`).
- Gained hands-on experience capturing real traffic, filtering by host, port, or protocol, and analyzing both live captures and saved `.pcap` files.
- Applied Tcpdump to identify specific network events, inspect protocols, and better understand packet structure and communication patterns.
