# Wireshark : The Basics

## Introduction
- Wireshark is an open-source, cross-platform network packet analyser tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP). It is commonly used as one of the best packet analysis tools. In this room, we will look at the basics of Wireshark and use it to perform fundamental packet analysis.


## Overview

### Concepts Learned
- Wireshark is a traffic analyser, useful for troubleshooting, detecting anomalies, and studying protocols.
- GUI has multiple key sections: Toolbar, Display Filter, Recent Files, Interfaces, Status Bar.
- PCAP files can be loaded to investigate captured traffic with three panes (list, details, bytes).
- Packets can be coloured (permanent or temporary) to quickly spot anomalies.
- Traffic sniffing is started/stopped via toolbar buttons.
- PCAP files can be merged into one for analysis.
- Capture file properties provide important metadata (hash, comments, stats).
- Hands-on work included analysing Exercise.pcapng to extract details.

### Explanation
- Use Cases: Wireshark is not an IDS but helps analyse packets. Effectiveness depends on the analyst.
**GUI Sections:**
  - Toolbar → filtering, exporting, merging.
  - Display Filter → queries.
  - Recent Files → quick access.
  - Interfaces → select sniffing point.
  - Status Bar → stats & profile info.
- PCAP Loading: Packets are shown in three panes: summary (list), breakdown (details), raw (bytes).
- Colouring: Protocols/anomalies can be highlighted with rules (session-only or profile-based).
- Sniffing: Blue shark = start, red = stop, green = restart.
- Merge: Combine multiple captures under File → Merge.
- File Details: Provides capture hash, timestamp, interface, comments.
- Hands-On: Extracted flag, total packets, and SHA256 from the lab-provided capture file.

### Notes
- Wireshark is a packet analysis tool useful for troubleshooting networks, detecting anomalies, and learning protocols.
- Captured traffic is displayed in three panes: packet list (summary), packet details (breakdown by layers), and packet bytes (raw data).
- Colouring rules help quickly identify protocol types or anomalies; they can be temporary (session) or permanent (profile-based).
- Capture files (PCAP/PCAPNG) can be opened, merged, or saved for later analysis.
- Capture file properties store metadata like timestamps, interfaces, comments, and file hashes, which are useful for validation.
- Wireshark is not an IDS; its effectiveness depends on the analyst’s interpretation of packet data.

## Packet Dissection

### Concepts Learned
- Packet dissection = protocol dissection, decoding packets into protocol fields using OSI layers.
- Wireshark supports dissecting many protocols, with the option to write custom dissectors.
- Packet details are broken down into 5–7 OSI-based layers.
- Each detail in the details pane highlights corresponding bytes in the raw pane.
**Key layers in dissection:**
  - Frame (Layer 1) → physical properties of the packet.
  - MAC (Layer 2) → source & destination MAC addresses.
  - IP (Layer 3) → source & destination IP addresses.
  - Protocol (Layer 4) → TCP/UDP, ports, transport details.
  - Protocol Errors → retransmissions/reassembly.
  - Application Protocol (Layer 5) → HTTP, FTP, SMB, etc.
  - Application Data (Layer 5 extension) → protocol-specific payload.

### Explanation
- Clicking a packet in the list pane reveals detailed breakdown.
- Each layer represents a step in the OSI model, from physical to application.
- Layer 1 (Frame): metadata like arrival time, frame size.
- Layer 2 (MAC): Ethernet addressing.
- Layer 3 (IP): network addressing, TTL, fragmentation.
- Layer 4 (Transport): TCP/UDP ports, sequence numbers.
- Errors: TCP reassembly or retransmission info.
- Layer 5 (Application Protocol): actual service-level protocol (HTTP, etc.).
- Application Data: raw payload contents (if not encrypted).
- Wireshark highlights bytes in the lower pane when selecting a field in the details pane, making it easier to map logical protocol data to physical bytes.

### Notes
- Packet dissection breaks down captured traffic into protocol layers for detailed analysis.
- Wireshark maps OSI layers to packet details: Frame → MAC → IP → Transport → Application → Payload.
- Selecting a field in the details pane highlights corresponding bytes in the raw pane, helping link protocol data to actual packet content.
- Protocol errors such as retransmissions or TCP reassembly can be detected at the transport layer.
- Application protocols (HTTP, FTP, SMB, etc.) and their payloads can be inspected in detail.
- Dissection allows analysts to investigate anomalies, verify protocol behavior, and understand packet structure.


## Packet Navigation

### Concepts Learned
- Each packet in Wireshark has a unique number for tracking.
- Analysts can navigate through packets using “Go to Packet” or search tools.
- Find, mark, and comment on packets to highlight and document events.
- Export packets and objects for focused or external analysis.
- Adjust time display formats for better event correlation.
- Expert Info highlights anomalies with severity categories.

### Explanation
- Packet Numbers: Identify and track packets in large captures.
- Go to Packet: Jump to specific packets or follow conversation flows.
- Find Packets: Search within packets using filters, hex, strings, or regex; scope depends on the selected pane.
- Mark Packets: Flag packets visually for follow-up; temporary per session.
- Packet Comments: Add persistent notes inside capture files for documentation.
- Export Packets/Objects: Extract selected packets or reconstructed files (HTTP, SMB, TFTP) for detailed analysis.
- Time Display Format: Switch between relative time or UTC for easier event analysis.
- Expert Info: Automated hints on anomalies like checksum errors, warnings, and protocol issues, categorized by severity.

### Notes
- Every packet has a unique number for easy reference in large captures.
- Analysts can navigate packets using “Go to Packet” to jump to specific numbers or conversation flows.
- Find Packets enables searching via display filters, strings, regex, or hex; search scope depends on the selected pane (list, details, or bytes).
- Marking packets visually flags them for follow-up, while comments persist in the capture for documentation.
- Packets or objects (e.g., files from HTTP, SMB, TFTP) can be exported for focused analysis.
- Time display format can be adjusted (e.g., seconds since capture start or UTC) for easier event correlation.
- Expert Info highlights potential anomalies such as checksum errors, deprecated protocol usage, or malformed packets, with severity categories (Chat, Note, Warn, Error).
- Navigation and annotation features improve efficiency, clarity, and collaboration during packet analysis.


## Packet Filtering

### Concepts Learned
- Wireshark supports capture filters (applied during packet capture) and display filters (applied while viewing captured packets).
- Apply as Filter: Quickly filter packets by a selected field/value.
- Conversation Filter: View all related packets between two endpoints (IP + ports).
- Colourise Conversation: Highlight related packets without filtering them out.
- Prepare as Filter: Build a filter query without applying it immediately.
- Apply as Column: Add specific packet fields as columns for easier analysis.
- Follow Stream: Reconstruct and view entire TCP/UDP/HTTP streams at the application level.

### Explanation
- Capture vs Display Filters: Capture filters restrict what packets are saved; display filters control what is visible in Wireshark.
- Apply as Filter: Generates a filter from a field/value and hides unrelated packets.
- Conversation Filter: Focuses on all packets in a conversation; ideal for tracing interactions between endpoints.
- Colourise Conversation: Changes packet colours for visual tracking of a conversation without hiding other packets.
- Prepare as Filter: Adds a query to the display filter bar for later execution, allowing complex conditions using AND/OR.
- Apply as Column: Enhances the packet list view to track specific fields across packets, such as ports, IPs, or flags.
- Follow Stream: Reconstructs communication streams, showing client/server traffic separately; useful to extract readable application data (e.g., HTTP requests, credentials).
- Filter Management: Applied filters can be cleared using the “X” button on the display filter bar to return to full packet view.

### Notes
- Filters help remove noise and focus on relevant packets.
- Applying conversation or stream filters is useful for investigating specific interactions.
- Columns can be added to track recurring packet fields across the capture.
- Streams reveal unencrypted application-level data for deeper analysis.


## Key Takeaways
- Wireshark is a versatile traffic analysis tool for troubleshooting, security analysis, and protocol learning.
- Packets are uniquely numbered, allowing easy reference and navigation in large captures.
- Packet dissection decodes traffic into OSI layers, revealing frame, MAC, IP, transport, protocol, and application data.
- Packet navigation features (Go to Packet, Find, Mark, Comment, Export) help efficiently investigate events and highlight anomalies.
- Filtering is essential to focus on relevant traffic using Display Filters, Apply/Prepare as Filter, Conversation Filter, Colourise, Columns, and Follow Stream.
- Colouring and columns improve visual clarity, enabling quick spotting of anomalies or protocol patterns.
- Streams reconstruction allows analysts to view application-level data, even unencrypted credentials or payloads.
- Expert Info and Time Display formats assist in spotting anomalies, errors, and understanding event timelines.
- Hands-on practice reinforced these concepts: loading PCAPs, dissecting packets, navigating captures, applying filters, reconstructing streams, marking/commenting, and extracting objects/files.
- Mastery of these tools improves network troubleshooting, security monitoring, and forensic analysis.
