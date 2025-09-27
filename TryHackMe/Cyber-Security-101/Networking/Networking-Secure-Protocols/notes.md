# Networking Secure Protocols

## Introduction
- This room focuses on securing communication over networks by addressing the limitations of core protocols. While protocols like HTTP, SMTP, POP3, and IMAP enable web browsing and email, they do not ensure confidentiality, integrity, or authenticity, leaving sensitive data such as passwords, payment details, and private documents exposed to potential attackers. To solve this, Transport Layer Security (TLS) is added to these protocols, creating secure versions like HTTPS, SMTPS, POP3S, and IMAPS.
- The room also introduces Secure Shell (SSH), which replaced the insecure Telnet protocol to provide safe remote access, along with Virtual Private Networks (VPNs), which establish secure tunnels over untrusted networks. Together, these technologies form the backbone of secure online communication, protecting both everyday use and critical transactions.


## Transport Layer Security (TLS)

### Concepts Learned
- Transport Layer Security (TLS) provides secure communication over insecure networks.
- TLS ensures confidentiality (nobody can read the data) and integrity (nobody can tamper with the data).
- TLS is the successor to SSL, with the latest version being TLS 1.3.
- Many protocols use TLS to add security: HTTPS, SMTPS, POP3S, IMAPS, DoT, MQTTS, SIPS.

### Explanation
- In the past, network traffic could be intercepted and read in cleartext using packet-capturing tools.
- TLS encrypts communication between clients and servers, preventing eavesdropping and tampering.
- Servers (or clients) obtain digital certificates signed by a Certificate Authority (CA) to prove their identity.
- Clients verify certificates against a pre-installed list of trusted CAs in browsers or operating systems.
- Free certificate services like Let’s Encrypt allow obtaining valid TLS certificates without cost.

### Notes
- TLS operates at the transport layer of the OSI model.
- Provides security for web traffic (HTTPS), email (SMTPS, POP3S, IMAPS), DNS (DoT), and other applications (MQTTS, SIPS).
- Certificate Authorities (CAs) verify and sign certificates, confirming the server or client identity.
- Self-signed certificates exist but are less trusted unless explicitly accepted by the client.


## Hypertext Transfer Protocol Secure

### Concepts Learned
- HTTPS is HTTP over TLS, providing secure web communication.
- TLS encrypts all HTTP traffic, ensuring confidentiality and integrity.
- HTTPS relies on TCP, TLS, and HTTP layered sequentially.

### Explanation
**Regular HTTP communication requires:**
  - TCP three-way handshake
  - HTTP request/response exchange
**HTTPS adds an additional step between TCP and HTTP:**
  - TCP three-way handshake
  - TLS session establishment (encryption setup)
  - HTTP request/response exchange over the encrypted channel
  - All HTTPS packets are encrypted, so intercepted traffic appears as gibberish.
  - Access to the private TLS key is required to decrypt the traffic for inspection.
  - TLS does not require changes to TCP, IP, or HTTP; it transparently adds security.

### Notes
- HTTPS traffic is typically on TCP port 443.
- TLS negotiation occurs after TCP connection and before HTTP communication.
- Packet capture tools like Wireshark show encrypted data as “Application Data” without the key.
- Decryption with the proper TLS key reveals the actual HTTP requests and responses.


## SMTPS, POP3S And IMAPS

### Concepts Learned
- TLS can secure email protocols just like HTTP, creating SMTPS, POP3S, and IMAPS.
- Secure versions of these protocols provide encryption for confidentiality and integrity.
- Almost all concepts from HTTPS (TLS handshake, encryption, packet confidentiality) apply here.

### Explanation
**Insecure protocols use default ports:**
  - HTTP → 80
  - SMTP → 25
  - POP3 → 110
  - IMAP → 143
**Secure protocols over TLS use default ports:**
  - HTTPS → 443
  - SMTPS → 465 and 587
  - POP3S → 995
  - IMAPS → 993
- TLS can be added to many other protocols in a similar fashion, providing the same advantages: encrypted communication, integrity, and authentication.

### Notes
- Switching from the insecure to secure version only changes the port and adds TLS; the underlying commands and usage remain the same.
- Encryption prevents attackers from intercepting sensitive data such as emails and passwords.
- The addition of TLS does not require changes to TCP or the application protocol itself.


## Secure Shell Protocol (SSH)

### Concepts Learned
- SSH is a secure replacement for TELNET, providing encrypted remote access.
- OpenSSH is the most common implementation of the SSH protocol.
- SSH ensures secure authentication, confidentiality, integrity, and can forward graphical applications (X11).

### Explanation
- SSH was developed in 1995 (SSH-1) and later upgraded to SSH-2 in 1996.
- SSH protects against eavesdropping and man-in-the-middle attacks.
- Supports multiple authentication methods: password, public key, and two-factor authentication.
- Can create secure tunnels for other protocols, functioning like a VPN.
- Allows X11 forwarding to run graphical applications remotely.
- SSH clients connect using ssh username@hostname or simply ssh hostname if the username matches.

### Notes
- TELNET is insecure because it sends credentials in cleartext; SSH encrypts all traffic.
- SSH listens on TCP port 22 (TELNET uses port 23).
- SSH enables secure remote administration and data transfer.
- Graphical applications can be forwarded using the -X option with an appropriate local graphical system.


## SFTP And FTPS

### Concepts Learned
- SFTP and FTPS are secure alternatives to FTP for transferring files.
- SFTP uses SSH for encryption, while FTPS uses TLS/SSL.

### Explanation
**SFTP (SSH File Transfer Protocol):**
  - Part of the SSH suite and uses TCP port 22.
  - Provides secure file transfer over an encrypted channel.
  - Commands resemble Unix shell commands (e.g., get, put).
**FTPS (File Transfer Protocol Secure):**
  - Secures FTP using TLS/SSL, similar to HTTPS.
  - Usually uses TCP port 990.
  - Requires proper TLS certificate setup.
  - Uses separate connections for control and data, which can complicate firewall configurations.

### Notes
- SFTP is simpler to enable via OpenSSH configuration.
- FTPS requires TLS certificates and careful firewall configuration.
- Both protocols ensure confidentiality and integrity of transferred files.
- SFTP and FTPS are recommended over traditional FTP for secure file transfers.


## Virtual Private Network (VPN)

### Concepts Learned
- VPNs create a secure, encrypted connection over the Internet between remote devices and a private network.
- VPNs are used to connect offices, employees, or devices to a main network as if they were physically local.

### Explanation
- Virtual: The network is built over the public Internet infrastructure.
- Private: The VPN encrypts traffic to ensure confidentiality and integrity.
- VPN clients connect to a VPN server, establishing a secure tunnel.
- Once connected, traffic can be routed through the VPN server, masking the user’s public IP and appearing as if coming from the server’s location.
- VPNs can help bypass geographical restrictions and provide secure access to corporate resources.
- Not all VPNs route all traffic; some only provide access to private networks.
- VPNs may leak the real IP address if misconfigured.
- Legal restrictions on VPN use exist in some countries.

### Notes
- VPNs require a server, client software, and Internet connectivity.
- All data passing through the VPN tunnel is encrypted.
- VPNs are widely used for remote work, secure Internet browsing, and circumventing content restrictions.
- Users should perform checks like DNS leak tests to ensure traffic is secure.
- Always verify local laws before using VPNs, especially when traveling.


## Hands On Practice

### Concepts Learned
- Three main approaches to securing network traffic were explored: TLS, SSH, and VPNs.
- Hands-on practice involved capturing and decrypting TLS traffic using Wireshark.

### Explanation
- TLS: Secures protocols like HTTP, SMTP, and POP3; secured protocols append “S” (HTTPS, SMTPS, POP3S).
- SSH: Provides secure remote access, file transfer, and tunneling for plaintext protocols.
- VPN: Encrypts traffic between devices or branches, providing secure remote network access.
- Wireshark can decrypt TLS traffic when provided with the browser’s TLS key log file.

### Notes
- To log TLS keys in the browser: chromium --ssl-key-log-file=~/ssl-key.log.
- TLS traffic can be decrypted in Wireshark by pointing it to the ssl-key.log file.
**Steps in Wireshark:**
- Right-click → Protocol Preferences → Transport Layer Security.
- Open Transport Layer Security preferences.
- Click Browse → select ssl-key.log → OK.
- Once configured, Wireshark displays decrypted TLS traffic, including potential login credentials.


## Key Takeaways
- TLS provides secure communication for many protocols without changing the underlying TCP/IP or application protocols. Protocols like HTTP, SMTP, POP3, and IMAP become HTTPS, SMTPS, POP3S, and IMAPS when secured.
- HTTPS is HTTP over TLS, encrypting web traffic to protect it from eavesdropping.
- SMTP, POP3, and IMAP can also be secured with TLS, with their default ports changing for secure versions.
- SSH provides secure remote access, encrypts traffic, ensures integrity, supports secure authentication, tunneling, and secure file transfer (SFTP).
- SFTP uses SSH (port 22) while FTPS uses TLS (port 990); both provide secure file transfers but via different mechanisms.
- VPNs allow secure connections over the Internet, encrypt traffic, and can mask the user’s public IP address.
- Hands-on practice with Wireshark and TLS key logs demonstrated how encrypted sessions are established and how traffic can be decrypted when keys are available.
- Securing network traffic ensures confidentiality, integrity, and authentication across different protocols and applications.
