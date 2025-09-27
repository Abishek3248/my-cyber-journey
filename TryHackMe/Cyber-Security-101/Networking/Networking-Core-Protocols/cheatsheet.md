# Cheatsheet - Networking Core Protocols

| Protocol | Purpose                         | Default Port(s) | Key Commands / Methods (examples)                                      |
|----------|---------------------------------|-----------------|------------------------------------------------------------------------|
| **HTTP** | Transfer web pages & resources  | 80 (TCP)        | GET (retrieve), POST (submit data), PUT (create/update), DELETE (remove) |
| **HTTPS**| Secure HTTP with encryption     | 443 (TCP)       | Same as HTTP, but encrypted with TLS/SSL                                |
| **FTP**  | File transfer between systems   | 21 (TCP, control) + dynamic data port | USER (username), PASS (password), RETR (download), STOR (upload), LIST (list files) |
| **SMTP** | Send emails from client → server and server → server | 25 (TCP)        | HELO/EHLO (initiate), MAIL FROM (sender), RCPT TO (recipient), DATA (send message), QUIT (end session) |
| **POP3** | Retrieve emails (download + delete, single device) | 110 (TCP)       | USER (username), PASS (password), STAT (status), LIST (list messages), RETR (retrieve), DELE (delete), QUIT (end) |
| **IMAP** | Retrieve & sync emails (multi-device, keeps messages on server) | 143 (TCP)       | LOGIN (authenticate), SELECT (choose mailbox), FETCH (retrieve mail), MOVE (move message), COPY (copy message), LOGOUT (end) |
