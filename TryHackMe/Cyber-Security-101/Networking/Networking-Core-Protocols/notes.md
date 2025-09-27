# Networking Core Protocols

## Introduction
- This room focuses on the essential core protocols that make communication across the Internet possible.
-  It introduces WHOIS for domain ownership lookup, DNS for translating domain names into IP addresses, HTTP and FTP for web and file transfers, and mail protocols such as SMTP, POP3, and IMAP for sending and receiving emails.
-   By working through these topics, you’ll gain both theoretical knowledge and practical experience in understanding how different services and applications rely on these protocols to function.


## Domain Name System (DNS)

### Concepts Learned
- DNS maps human-friendly domain names to IP addresses (and other records), removing the need to memorize numeric addresses.
- DNS runs at the Application layer and primarily uses UDP port 53 (TCP 53 as fallback or for zone transfers/large responses).
- Common DNS record types: A (IPv4), AAAA (IPv6), CNAME (alias to another name), MX (mail exchanger).

### Explanation
- When an application (e.g., a web browser or mail server) needs an IP for a name, it queries a DNS resolver which returns the requested record (A, AAAA, MX, etc.).
**Typical record roles:**
  - A — maps a hostname to one or more IPv4 addresses.
  - AAAA — maps a hostname to one or more IPv6 addresses.
  - CNAME — maps a hostname to another hostname (alias).
  - MX — specifies the mail server(s) for a domain.
- Example flow: resolving www.example.com may produce an A answer (IPv4) and an AAAA answer (IPv6); each query/response is visible on the wire (e.g., via tshark or tcpdump).
- Tools like nslookup, dig, and host perform DNS lookups from the command line and are useful for troubleshooting and inspection.

### Notes
- DNS responses may be authoritative (from the domain’s authoritative server) or non‑authoritative (from a recursive resolver/cache).
- DNS uses UDP for typical queries because it’s lightweight; if a response is too large or TCP is explicitly required (e.g., zone transfers), the query falls back to TCP.
- CNAMEs should not coexist with other record types for the same name (common DNS best-practice).
- DNS is a frequent reconnaissance target in pentesting: look for public records (A/AAAA/CNAME/MX), subdomains, and misconfigurations (e.g., exposed internal names, wildcard records, or leftover DNS entries).
- Packet captures show query/response pairs (example: client → resolver: A query; resolver → client: A answer). Use nslookup/dig +trace and packet captures to debug full resolution paths.


## WHOIS

### Concepts Learned
- WHOIS provides public information about the entity that registered a domain name.
- It helps determine domain ownership, registration date, expiration date, registrar, and contact details.
- Useful in cybersecurity for reconnaissance, tracking abuse, or verifying domain legitimacy.

### Explanation
- Every registered domain has a WHOIS record maintained by the domain registrar.
- Registrants must provide accurate contact information, though privacy/proxy services can hide this information from public queries.
**Common fields in a WHOIS record:**
  - Domain Name
  - Registry Domain ID
  - Registrar and WHOIS server
  - Creation, update, and expiration dates
  - Registrant name, organization, address, email, and phone (may be protected by privacy services)
**Usage**
  - Command-line tool: whois example.com
  - Online WHOIS lookup services are also available.
  - Privacy services can mask registrant details to protect personal information.

### Notes
- WHOIS data is helpful for investigating domain ownership and history.
- Some TLDs and registrars enforce stricter privacy rules, limiting exposed information.
- Not all fields are standardized across TLDs; some records may include additional technical or administrative contacts.


## HTTP(S) - Web Access

### Concepts Learned
- HTTP (Hypertext Transfer Protocol) and HTTPS (HTTP Secure) are the main protocols for web communication.
- HTTPS secures HTTP traffic using TLS/SSL encryption.
- Web communication relies on TCP, typically using ports 80 (HTTP) and 443 (HTTPS).

### Explanation
- HTTP defines how web browsers and servers communicate. Browsers issue requests to retrieve or submit data, while servers respond with the requested content and additional metadata (headers).
**Common HTTP methods include:**
  - GET: Retrieve data (HTML, images, files).
  - POST: Submit data (forms, uploads).
  - PUT: Create or update resources.
  - DELETE: Remove resources.
-Communication includes more than visible page content; headers may reveal server info, content type, cookies, and timestamps. Tools like Wireshark can capture and inspect these exchanges to study requests and responses.

### Notes
- Telnet or similar TCP clients can manually send HTTP requests for troubleshooting:
   *GET / HTTP/1.1
   Host: example.com*
- Specific files can be requested by adjusting the GET path (GET /file.html HTTP/1.1).
- HTTP is unencrypted, while HTTPS ensures confidentiality and integrity of the data exchanged.


## File Transfer Protocol (FTP)

### Concepts Learned
- FTP (File Transfer Protocol) is designed for transferring files between a client and server.
- FTP uses two TCP connections: one for control (commands) on port 21, and another for data transfer.
- Supports authentication (username/password) and file operations.

### Explanation
**FTP allows clients to efficiently upload and download files. Key FTP commands include:**
  - USER: Provide the username.
  - PASS: Provide the password.
  - RETR: Retrieve/download a file from the server.
  - STOR: Upload a file to the server.
  - ls / LIST: List files in the current directory.
  - type ascii / binary: Set transfer mode.
- FTP establishes a control connection to send commands and a separate data connection for transferring files or directory listings. This separation allows for simultaneous command and file transfer operations.

### Notes
- Anonymous login is possible if the server allows it; a username like anonymous is used, often without a password.
-  Commands are sent over the control channel, while the file content or directory listings are sent over a new data connection.
**Example session steps:**
  - Connect to server: ftp <server-ip>
  - Log in: USER anonymous
  - List files: ls
  - Set mode (ASCII for text): type ascii
  - Download file: get coffee.txt
  - Exit: quit
- Wireshark can capture the FTP control and data exchanges; client commands appear in red and server responses in blue.


## Simple Mail Transfer Protocol (SMTP)

### Concepts Learned
- SMTP (Simple Mail Transfer Protocol) is used for sending emails between clients and servers, and between mail servers themselves.
- It operates over TCP port 25 by default.
- The protocol uses text-based commands to define the sender, recipient, and message content.

### Explanation
- SMTP works much like mailing a package at a post office: you greet the server, provide sender and recipient details, and then hand over the “package” (the email message).
**Common commands include:**
  - HELO / EHLO – Initiates a session with the server.
  - MAIL FROM: – Specifies the sender’s email address.
  - RCPT TO: – Specifies the recipient’s email address.
  - DATA – Indicates the start of the message body.
  - . (dot on its own line) – Ends the message.
  - QUIT – Closes the session.

### Notes
- A typical SMTP session involves:
- Client connects to server (usually port 25).
- Initiates greeting with HELO or EHLO.
- Provides sender’s email with MAIL FROM.
- Defines recipient with RCPT TO.
- Sends message content after DATA, ending with a . on a separate line.
- Ends session with QUIT.
- Tools like telnet can be used to manually simulate an SMTP session for learning or troubleshooting.
- In Wireshark, SMTP traffic shows client commands in red and server responses in blue.
- While using telnet is impractical for real use, it helps visualize what email clients do automatically under the hood.


## Post Office Protocol v3 (POP3)

### Concepts Learned
- POP3 (Post Office Protocol v3) is used by mail clients to retrieve emails from a mail server.
- It works over TCP port 110 by default.
- SMTP is used to send emails, while POP3 is used to download them.

### Explanation
- POP3 functions like checking your mailbox: once the email is retrieved, it’s available on your local system, and in many cases removed from the server.
**Common commands include:**
  - USER <username> – identifies the user
  - PASS <password> – authenticates with the server
  - STAT – shows number and size of messages
  - LIST – lists all messages with their sizes
  - RETR <message_number> – downloads a specific message
  - DELE <message_number> – marks a message for deletion
  - QUIT – ends the session and applies changes

### Notes
**A POP3 session typically involves:**
  - Client connects to server on port 110.
  - Provides username (USER) and password (PASS).
  - Requests mailbox info with STAT or LIST.
  - Retrieves messages with RETR.
  - Marks unwanted messages with DELE.
  - Ends session with QUIT.
- POP3 traffic is plain text by default — usernames, passwords, and message content can be intercepted easily.


## Internet Message Access Protocol (IMAP)

### Concepts Learned
- IMAP (Internet Message Access Protocol) is used to synchronize emails across multiple devices.
- Unlike POP3, which downloads and often deletes emails from the server, IMAP keeps them on the server and syncs changes (read, moved, deleted) across clients.
- Default port: TCP 143.

### Explanation
- IMAP is ideal when accessing emails from multiple devices (desktop, laptop, smartphone).
- Emails remain stored on the server, which ensures consistency across clients.
- More storage is usually needed since emails are not deleted after retrieval.
- IMAP commands are more advanced and allow managing mailboxes and messages directly on the server.
**Common IMAP Commands**
  - LOGIN <username> <password> – authenticates user
  - SELECT <mailbox> – selects a mailbox (e.g., inbox)
  - FETCH <mail_number> <data_item_name> – retrieves message data (e.g., FETCH 3 body[])
  - MOVE <sequence_set> <mailbox> – moves messages to another folder
  - COPY <sequence_set> <mailbox> – copies messages
  - LOGOUT – ends the session

### Notes

**Typical IMAP session steps:**
  - Client connects to server on port 143.
  - Logs in using LOGIN.
  - Selects mailbox with SELECT.
  - Retrieves messages using FETCH.
  - Moves or copies messages if needed.
  - Ends session with LOGOUT.
**Compared to POP3:**
  - POP3 = personal mailbox (download & delete).
  - IMAP = shared synchronized mailbox (server-stored).
-Like POP3, IMAP also communicates in plain text by default → usernames, passwords, and message content are visible to packet sniffers (seen in Wireshark captures).


## Key Takeaways
- Protocols act as rulebooks that define how data is exchanged between clients and servers.
- HTTP is the backbone of the web, mainly used for delivering websites and resources.
- FTP is designed for transferring files between client and server and is more efficient than HTTP for file movement.
- SMTP handles the process of sending emails from clients to servers and between servers.
- POP3 allows users to download emails from the server, best suited for single-device use.
- IMAP keeps emails stored on the server and synchronizes them across multiple devices, making it more flexible than POP3.
- Protocols like HTTP, FTP, SMTP, POP3, and IMAP are text-based and easily readable in network captures.
- Using them without encryption exposes sensitive data such as usernames, passwords, and email contents.
- Secure alternatives (HTTPS, FTPS, SMTPS, IMAPS, POP3S) are essential to protect communication from eavesdropping.
