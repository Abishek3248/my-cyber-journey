# Cheatsheet - Wireshark Quicklook

| Feature / Concept            | Description / Usage                                                                 |
|-------------------------------|-----------------------------------------------------------------------------------|
| **Packet Numbers**            | Unique IDs for each packet; use for navigation and referencing.                    |
| **Packet Dissection**         | Decodes packets into OSI layers: Frame, MAC, IP, Transport, Protocol, App Data.   |
| **Packet Navigation**         | - Go to Packet: jump to specific packet. <br> - Find: search by display filter, hex, string, regex. <br> - Mark: highlight packets visually. <br> - Comments: add persistent notes. <br> - Export Packets/Objects: extract packets/files for focused analysis. |
| **Filtering**                 | - Display vs Capture filters. <br> - Apply as Filter, Prepare as Filter. <br> - Conversation Filter & Colourise. <br> - Apply as Column. <br> - Follow Stream (TCP/UDP/HTTP). |
| **Colouring Rules**           | Temporary (session-only) or Permanent (profile-based) to highlight protocols/anomalies. |
| **Streams**                   | Reconstructs application-level data for TCP/UDP/HTTP streams; identifies client/server traffic. |
| **Time Display Format**       | Adjust timestamps: Seconds Since Start or UTC for easier correlation.             |
| **Expert Info**               | Automated hints on anomalies: Chat (blue), Note (cyan), Warn (yellow), Error (red). |
| **PCAP Handling**             | - Load files via drag/drop or File menu. <br> - Merge multiple PCAPs. <br> - View capture file properties (hash, comments, stats). |
| **Hands-On Lab Tasks**        | Loading PCAPs, dissecting packets, navigating captures, applying filters, marking/commenting, stream following, exporting packets/objects. |


