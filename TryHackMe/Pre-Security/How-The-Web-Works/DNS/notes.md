# DNS (Domain Name System)

## Introduction
- The Domain Name System (DNS) makes the internet user-friendly by translating human-readable names (like tryhackme.com) into machine-readable IP addresses (like 104.26.10.229). Instead of memorizing long numerical addresses, DNS allows us to access websites through simple domain names, much like using a house address instead of geographical coordinates.


## Domain Hierarchy

### Concepts Learned
- Structure of domain names (Root → TLD → Second-Level → Subdomains).
- Different types of TLDs: Generic (gTLD) and Country Code (ccTLD).
- Rules and restrictions for creating second-level domains and subdomains.

### Explanation
- TLD (Top-Level Domain): The rightmost part of a domain (e.g., .com in tryhackme.com).
- gTLDs: Indicate purpose (e.g., .com = commercial, .org = organization).
- ccTLDs: Represent country/region (e.g., .ca = Canada, .co.uk = UK).
- Today, many new gTLDs exist (e.g., .online, .club, .biz).
- Second-Level Domain: The part before the TLD (e.g., tryhackme in tryhackme.com).
- Rules: Up to 63 characters, only letters (a–z), numbers (0–9), and hyphens.
- Restrictions: Cannot start/end with hyphens or use consecutive hyphens.
- Subdomain: Placed before the second-level domain, separated by a dot.
- Example: admin.tryhackme.com → admin is the subdomain.
- Multiple subdomains can be chained (e.g., jupiter.servers.tryhackme.com).
- Rules: Same as second-level domains, with total length ≤ 253 characters.
- No limit on the number of subdomains.

### Notes
- Root domain (at the very top of the hierarchy) is usually represented by an empty dot (.).
- Subdomains are often used to organize services (e.g., mail.google.com, drive.google.com).


## DNS Record Types

### Concepts Learned
- DNS supports different record types beyond just mapping websites to IPs.
- Each record type serves a specific function, such as resolving addresses, handling email, or verifying domain ownership.

### Explanation
- A Record → Maps a domain to an IPv4 address (e.g., 104.26.10.229).
- AAAA Record → Maps a domain to an IPv6 address (e.g., 2606:4700:20::681a:be5).
- CNAME Record → Points a domain to another domain name (e.g., store.tryhackme.com → shops.shopify.com).
- MX Record → Specifies mail servers for the domain, with priorities for failover (e.g., alt1.aspmx.l.google.com).
- TXT Record → Stores text data for various uses, such as:
- Email authentication (SPF, DKIM).
- Verifying domain ownership with third-party services.

### Notes
- A & AAAA records directly resolve to IPs.
- CNAME is an alias; requires another DNS lookup.
- MX records are critical for reliable email delivery.
- TXT records provide flexibility, widely used in security and verification.

## Making a DNS Request

### Concepts Learned
- DNS resolution involves multiple steps, starting from local cache and moving outward if needed.
- Recursive, root, TLD, and authoritative servers each play a role in finding the correct IP.
- Caching improves efficiency and reduces repeated lookups.

### Explanation
- Computer checks local DNS cache first.
- If not found, query goes to a Recursive DNS Server (usually ISP-provided).
- Recursive server checks its own cache; if no match → forwards request.
- Root DNS Servers redirect the query to the correct TLD server (e.g., .com).
- TLD server points to the authoritative nameserver for the domain.
- Authoritative server returns the actual DNS record (e.g., A, MX, etc.).
- Recursive server caches the response for its TTL (Time To Live) duration and returns it to the client.

### Notes
- Root servers act as the backbone, handling redirection only.
- TLD servers manage addresses under specific extensions like .com, .org, .net.
- Authoritative servers are the final source of truth for DNS records.
- TTL defines how long a cached entry is valid before a new lookup is required.

## Practical

### Concepts Learned
- Learned how to perform DNS lookups both through a web-based tool (GUI) and the command line.
- Discovered that nslookup is a common command to manually query DNS records.

### Explanation
- The exercise involved using a browser-based interface to make DNS queries and view results.
- The tool also displayed the equivalent terminal command for each query, helping bridge practical GUI usage and real CLI execution.
- Practiced identifying different DNS record types (CNAME, TXT, MX, A) and their values for a given domain.

### Notes
- Command used: nslookup <domain> → fetches DNS records.
 **Practiced queries and results:**
- CNAME of shop.website.thm → shops.myshopify.com
- TXT record of website.thm → THM{7012BBA60997F35A9516C2E16D2944FF}
- MX record priority → 30
- A record of www.website.thm → 10.10.10.10


## Key Takeaways
- DNS simplifies communication by mapping human-readable domain names to IP addresses.
- Domains follow a hierarchy: root → TLD → second-level domains → subdomains.
- DNS records (A, AAAA, CNAME, MX, TXT) serve different purposes like IP mapping, mail routing, and domain verification.
- DNS requests may resolve locally (cache) or traverse recursive, root, TLD, and authoritative servers.
- Caching and TTL values reduce repeated lookups and improve efficiency.
- Practical tools like nslookup allow querying DNS records directly.
