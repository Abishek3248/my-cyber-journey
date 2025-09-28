# Tcpdump Basics

## Introduction
- tcpdump is a packet sniffing and packet analyzing tool for a System Administrator to troubleshoot connectivity issues in Linux. It is used to capture, filter, and analyze network traffic such as TCP/IP packets going through your system.
-  It is many times used as a security tool as well. It saves the captured information in a pcap file, these pcap files can then be opened through Wireshark or through the command tool itself.


## Basic Packet Capture

### Concepts Learned
- Tcpdump requires choosing the correct network interface to capture traffic.
- Captured packets can be saved to a file and later re-read for analysis.
- It’s possible to limit the number of packets during a capture.
- Disabling DNS and port resolution avoids extra lookups and speeds up output.
- Captures can be displayed with varying levels of verbosity for more detail.

### Explanation
- List Interfaces → ip a s shows available network interfaces.
- Capture on Interface → tcpdump -i INTERFACE (or -i any for all).
- Save Captures → tcpdump -w FILE.pcap (no live output shown).
- Read Captures → tcpdump -r FILE.pcap.
- Limit Packets → tcpdump -c COUNT.
**Disable Resolution:**
  - -n → don’t resolve IPs.
  - -nn → don’t resolve IPs or ports.
**Verbosity:**
  - -v → more details.
  - -vv → even more.
  - -vvv → maximum verbosity.

### Notes
- Checked available interfaces (lo and ens5).
- Captured 5 packets on ens5 with -c 5 -n.
- Saved traffic to capture.pcap with -w, later re-read using -r.
- Captured across all interfaces using -i any.
- Compared packet details at different verbosity levels (-v, -vv).
- Observed the difference between raw IPs/ports vs resolved names when using -n and -nn.


## Filtering Expressions

### Concepts Learned
- Filtering is essential in tcpdump to focus only on relevant traffic.
- Filters can be based on host (IP or hostname), port, or protocol.
- Source (src) and destination (dst) keywords refine filtering by direction.
- Logical operators (and, or, not) allow combining conditions for precise captures.
- Filtering helps reduce noise and makes packet analysis efficient.

### Explanation
**Filter by Host:**
  - tcpdump host IP/HOSTNAME → capture packets to/from a host.
  - tcpdump src host IP → packets from a specific source.
  - tcpdump dst host IP → packets to a specific destination.
**Filter by Port:**
  - tcpdump port PORT → all packets on a given port.
  - tcpdump src port PORT → from a source port.
  - tcpdump dst port PORT → to a destination port.
**Filter by Protocol:**
  - tcpdump PROTOCOL (e.g., icmp, ip, ip6, tcp, udp).
**Logical Operators:**
  - and → both conditions must match.
  - or → either condition matches.
  - not → exclude packets matching condition.
**Reading Captures with Filters:**
  - tcpdump -r FILE FILTER → apply filters on saved packet captures.

### Notes
- Practiced capturing HTTP traffic with host example.com.
- Tested DNS traffic filtering using port 53 (saw A and AAAA queries).
- Captured ICMP echo requests/replies and time exceeded messages.
- Verified HTTPS capture with combined filter host example.com and tcp port 443.
- Used wc to count filtered packets (910 packets from 192.168.124.1).
- Filtering greatly reduces packet noise and isolates traffic of interest.


## Advanced Filtering

### Concepts Learned
- Filtering can also be based on packet length, allowing capture of packets larger or smaller than a threshold.
- Binary operations (&, |, !) help build advanced filtering logic.
- Tcpdump can filter based on protocol header bytes using the format proto[expr:size].
- This allows inspection of specific header fields (e.g., Ethernet, IP, TCP).
- Advanced use case: filtering packets by TCP flags (SYN, ACK, FIN, RST, PUSH).
- Combining logical operators and flag checks makes it possible to precisely isolate traffic of interest.

### Explanation
**Filter by Length**
  - tcpdump greater LENGTH → packets ≥ specified length.
  - tcpdump less LENGTH → packets ≤ specified length.
**Binary Operations**
  - & (AND) → both conditions must be true.
  - | (OR) → either condition true.
  - ! (NOT) → invert/exclude condition.
**Header Byte Filtering**
  - Syntax: proto[expr:size]
  - proto → protocol (ether, ip, ip6, tcp, udp, etc.).
  - expr → byte offset (0 = first byte).
  - size → number of bytes (1, 2, or 4).
**Example:**
  - ether[0] & 1 != 0 → filter multicast Ethernet packets.
  - ip[0] & 0xf != 5 → catch IP packets with options.
**TCP Flags Filtering**
  - tcpdump "tcp[tcpflags] == tcp-syn" → packets with only SYN set.
  - tcpdump "tcp[tcpflags] & tcp-syn != 0" → packets with at least SYN set.
  - tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0" → packets with SYN or ACK set.

### Notes
- Practiced filtering based on packet length to separate small vs large packets.
- Reviewed binary operations logic (&, |, !) and applied in tcpdump expressions.
- Tested header byte filtering with ether[0] and ip[0] examples.
- Focused on TCP flags: successfully captured SYN packets during a 3-way handshake.
- Verified ACK filtering to track established connections.
- Advanced filtering allows extremely precise packet capture when working with large datasets.


## Displaying Packets

### Concepts Learned
- Tcpdump provides multiple options to customize packet display depending on the analysis needs.
- Quick output gives shorter, cleaner lines for a high-level view.
- Link-level headers (-e) allow inspection of MAC addresses, useful for ARP/DHCP and tracking unusual traffic sources.
- ASCII view (-A) displays readable text when packet payloads contain plain text.
- Hexadecimal view (-xx) reveals raw packet contents, independent of encoding or language.
- Combined view (-X) shows both hex and ASCII, providing the most detailed inspection.

### Explanation
- tcpdump -q → Quick output (brief info: IPs, ports, sizes).
- tcpdump -e → Include MAC addresses and link-level headers.
- tcpdump -A → Display packet data as ASCII characters.
- tcpdump -xx → Display packets in hexadecimal format.
- tcpdump -X → Show both hex and ASCII views together.

### Notes
- Practiced using -q to simplify clutter in large captures.
- Used -e to analyze Ethernet headers and verify MAC addresses.
- Applied -A to view readable text in HTTP traffic.
- Switched to -xx when inspecting binary/encrypted payloads.
- Found -X most effective when reviewing headers + payload simultaneously.
- Choosing the right display option depends on the protocol being analyzed and the investigation’s goal.


## Key Takeaway
- Learned how to capture packets effectively with tcpdump and apply filters to reduce noise.
- Practiced filtering by host, port, protocol, and TCP flags to target specific traffic.
- Explored advanced filtering using binary operations and header bytes for precise analysis.
- Understood different display options (-q, -e, -A, -xx, -X) to view packets in summary, ASCII, hex, or combined formats.
- Gained hands-on experience with reading, saving, and analyzing packet captures.
- Built confidence in using tcpdump as a powerful CLI tool for real-world network troubleshooting and analysis.
