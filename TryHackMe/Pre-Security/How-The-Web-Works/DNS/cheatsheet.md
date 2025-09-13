# Cheatsheet – DNS

| Record / Concept   | Purpose / Responsibility                                           | Example / Notes                                                                 |
|--------------------|-------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **A Record**       | Maps domain → IPv4 address                                        | `tryhackme.com → 104.26.10.229`                                                 |
| **AAAA Record**    | Maps domain → IPv6 address                                        | `example.com → 2606:4700:20::681a:be5`                                          |
| **CNAME Record**   | Alias: maps one domain → another domain                           | `shop.website.thm → shops.myshopify.com`                                        |
| **MX Record**      | Defines mail servers for a domain; includes priority              | `alt1.aspmx.l.google.com (priority 30)`                                         |
| **TXT Record**     | Stores text data for verification, SPF, DKIM, ownership           | `THM{7012BBA60997F35A9516C2E16D2944FF}`                                         |
| **Subdomain**      | Prefix to second-level domain; used for services/organization     | `admin.tryhackme.com`, `jupiter.servers.tryhackme.com`                          |
| **Recursive DNS**  | First stop for queries; usually ISP or custom (e.g. 8.8.8.8)      | Checks cache before querying further                                            |
| **Root Servers**   | Directs queries to appropriate TLD servers                        | `.com`, `.org`, `.net`, etc.                                                    |
| **TLD Server**     | Holds records for authoritative servers of domains under its TLD  | `.com → Cloudflare NS for tryhackme.com`                                        |
| **Authoritative NS** | Stores DNS records for a domain; final source of truth           | `kip.ns.cloudflare.com`, `uma.ns.cloudflare.com`                                |
| **TTL (Time To Live)** | Lifetime (in seconds) a record is cached before refresh        | Improves performance by reducing repeated lookups                               |
| **Tool: nslookup** | Command-line tool to query DNS records                            | `nslookup -type=A www.website.thm`                                              |

