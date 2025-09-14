# Cheatsheet - Putting It All Together

## Web Request Flow

| Step | Description |
|------|-------------|
| 1. URL Request | User enters a URL in the browser. |
| 2. DNS Resolution | Browser asks DNS server for the IP of the domain. |
| 3. TCP Connection | Browser establishes connection to the web server (HTTPS adds TLS handshake). |
| 4. HTTP Request | Browser sends HTTP/HTTPS request (GET, POST, etc.) to the server. |
| 5. Web Server Processing | Server processes request; dynamic content handled by backend scripts. |
| 6. Database Query | Server may query database for requested data. |
| 7. Response Generated | Server sends back HTML, CSS, JS, images, etc. |
| 8. Rendering | Browser renders frontend using received content. |
| 9. Additional Requests | Browser may request additional resources (images, scripts, etc.). |

## Web Components

| Component | Purpose |
|-----------|---------|
| Load Balancer | Distributes incoming requests across multiple servers to ensure high availability. |
| CDN (Content Delivery Network) | Hosts static assets closer to users for faster delivery and reduced server load. |
| Web Server | Handles incoming HTTP/HTTPS requests and serves files or dynamic content. |
| Database | Stores and retrieves user and application data. |
| WAF (Web Application Firewall) | Protects against malicious requests, attacks, and rate limits excessive traffic. |

## Web Server Concepts

| Concept | Notes |
|---------|-------|
| Virtual Hosts | Host multiple websites on a single server; routing based on requested hostname. |
| Static Content | Files served directly from server without modification (images, CSS, JS, fixed HTML). |
| Dynamic Content | Generated on-the-fly by backend scripts (PHP, NodeJS, Python, etc.). |
| Backend Languages | Handle dynamic content, database queries, and business logic. |

## Security & Optimization

| Mechanism | Purpose |
|-----------|---------|
| WAF | Detects attacks, filters malicious requests, rate limits traffic. |
| Load Balancer Health Checks | Ensures only healthy servers receive traffic. |
| CDN | Reduces latency and server load by delivering content from nearest location. |
| Secure Backend Practices | Avoid exposing sensitive data, sanitize inputs, manage sessions securely. |

