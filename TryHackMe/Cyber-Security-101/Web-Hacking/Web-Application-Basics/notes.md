# Web Application Basics

## Introduction
**Topics Covered**
- Understand what a web application is and how it runs in a web browser.
- Break down the components of a URL and see how it helps access web resources.
- Learn how HTTP requests and responses work.
- Get familiar with the different types of HTTP request methods.
- Understand what different HTTP response codes mean.
- Check out how HTTP headers work and why they matter for security.


## Web Application Overview

### Concepts Learned
- Understand the structure and components of a web application.
- Recognize the distinction between Front End and Back End.
- Learn the purpose of Web Application Firewalls (WAF) in securing web apps.

### Explanation
- A web application can be compared to a planet:
- Front End = surface visible to users, built with HTML, CSS, and JavaScript.
- Back End = unseen infrastructure supporting the application, including servers, databases, and security layers.
**Front End**
*HTML (Hypertext Markup Language):*
- Provides structure and content to the web page.
- Analogy: DNA of simple organisms on a planet.
*CSS (Cascading Style Sheets):*
- Adds styling, colors, layouts, and visual design to HTML.
- Analogy: DNA specifying the appearance, size, shape, and color.
*JavaScript (JS):*
- Adds interactivity and logic to web pages.
- Analogy: Brain of an organism making decisions based on interaction.
**Back End**
*Database:*
- Stores, retrieves, and modifies application data (e.g., user preferences).
- Analogy: Libraries, diaries, or filing systems on a planet.
*Infrastructure:*
- Includes web servers, application servers, networking devices, and storage.
- Analogy: Roads, cars, and fuel powering the planet’s ecosystem.
*Web Application Firewall (WAF):*
- Protects the application from malicious requests.
- Analogy: Planet’s atmosphere shielding inhabitants from harmful elements.

### Notes
- Front End affects user experience and runs in the browser.
- Back End is critical for functionality and may include security features like WAF.
- HTML, CSS, and JS should be understood to manipulate or analyze web applications during testing.
- Databases and servers are common points of interest during penetration testing or vulnerability assessment.


## Uniform Resource Locator (URL)

### Concepts Learned
- A URL is a web address that directs a browser to online resources (webpages, images, videos, etc.).
- A URL is made up of multiple components: scheme, user, host/domain, port, path, query string, and fragment.
- Each part has a specific purpose in accessing and securing resources.
- URLs can be abused in attacks like typosquatting or injection via query strings and fragments.

### Explanation
- Scheme: Defines the protocol (HTTP, HTTPS). HTTPS is secure due to encryption and is recommended for protection.
- User: Can include login credentials in rare cases, but unsafe since it exposes sensitive information.
- Host/Domain: Identifies the website. Must be unique. Attackers exploit lookalike domains (typosquatting) for phishing.
 **Port: Specifies the communication endpoint. Common:**
   - 80 → HTTP
   - 443 → HTTPS
- Path: Shows the specific file/page on the server. Sensitive paths must be restricted to authorized users.
- Query String: Begins with ? and carries user input (e.g., search terms, form data). Must be validated to avoid injection attacks.
- Fragment: Begins with # and points to a section of the page (e.g., headings). Can also be tampered with, so sanitization is important.

### Notes
- Always check if a site enforces HTTPS for secure communication.
- Typosquatting is a major phishing risk — e.g., g00gle.com vs google.com.
- Ports outside defaults (80/443) can indicate non-standard services; good to check during recon.
- Query strings & fragments = user-controlled input → must be sanitized to prevent injections.
**Useful mental model:**
  - scheme://user@host:port/path?query#fragment
**Example:**
  - https://user@site.com:443/docs/page?search=test#section2
 

## HTTP Messages

### Concepts Learned
- HTTP messages are packets of data exchanged between the client (user) and the server.
**Two types:**
  - HTTP Requests → sent by the client to trigger actions (e.g., login, fetch a page).
  - HTTP Responses → sent by the server back to the client.
- Each message follows a standard format: Start Line → Headers → Empty Line → Body.
- Correct structure ensures smooth communication and prevents misinterpretation.

### Explanation
**Start Line:**
  - Request → includes method, target URL, and HTTP version.
  - Example: POST /login HTTP/1.1
  - Response → includes status code and reason phrase.
  - Example: HTTP/1.1 200 OK
**Headers:**
  - Key-value pairs providing metadata (e.g., Content-Type:, User-Agent:, Authorization:).
  - Help control behavior, security, and formatting.
**Empty Line:**
  - Separates headers from body.
  - Without it, client/server may misinterpret where data starts.
**Body:**
  - Request body → carries user data (form fields, JSON, etc.).
  - Response body → carries server output (HTML page, JSON API response, etc.).

### Notes
**HTTP Request Example:**
  - "POST /login HTTP/1.1
     Host: example.com
     Content-Type: application/x-www-form-urlencoded
     Content-Length: 27"
  - username=admin&password=1234
**HTTP Response Example:**
  - "HTTP/1.1 200 OK
    Content-Type: text/html
    Content-Length: 123"
  - <html><body>Login Successful</body></html>
- Understanding HTTP messages is critical for debugging web issues (e.g., wrong headers, malformed body).
- Security relies heavily on correct handling of messages (e.g., preventing header injection, validating body data).
- An attacker may tamper with headers, queries, or body data → leading to exploits like XSS, SQLi, CSRF.


## HTTP Request: Request Line and Methods

### Concepts Learned
- HTTP requests are the main way a client interacts with a web server.
- The Request Line defines the action (method), resource (path), and protocol (version).
- Different HTTP methods serve different purposes but can also introduce security risks if misused.
- The URL path identifies resources and must be validated to prevent exploitation.
- Understanding HTTP versions is important for performance and security.

### Explanation
**Request Line**
**Structure:**
  - METHOD /path HTTP/version
**Example:**
  - GET /login HTTP/1.1
**Parts:**
  - Method → action (GET, POST, etc.)
  - Path → resource being requested
  - Version → HTTP protocol version
**HTTP Methods**
  - GET → fetches data (no changes). Risk: sensitive data in URL.
  - POST → sends data to create/update. Risk: injection attacks if input not validated.
  - PUT → updates/replaces resource. Risk: improper authorization.
  - DELETE → removes resource. Risk: must enforce strict authorization.
  - PATCH → partial update. Risk: input validation needed.
  - HEAD → returns headers only. Useful for metadata checks.
  - OPTIONS → shows allowed methods. Risk: information disclosure.
  - TRACE → echoes request for debugging. Risk: leaks sensitive headers.
  - CONNECT → establishes tunnels (used for HTTPS).
**URL Path**
  - Example: /api/users/123 → targets user with ID 123.
**Security practices:**
  - Validate & sanitize paths.
  - Prevent path traversal & forced browsing.
  - Avoid leaking sensitive info in paths.
**HTTP Versions**
  - HTTP/0.9 → only GET supported.
  - HTTP/1.0 → headers introduced.
  - HTTP/1.1 → persistent connections, caching (still widely used).
  - HTTP/2 → multiplexing, compression, better performance.
  - HTTP/3 → based on QUIC, faster and more secure.

### Notes
- The request line sets the intent of the client.
- Weak handling of HTTP methods (e.g., PUT/DELETE left open) creates vulnerabilities.
- Path validation is key to preventing unauthorized access.
- Upgrading to newer HTTP versions improves speed and security.


## HTTP Request: Headers and Body

### Concepts Learned
- Request headers carry metadata about the request (host, client, cookies, content type, etc.).
- The request body carries data for methods like POST/PUT; its format depends on Content-Type.
- Common body formats: URL-encoded, multipart/form-data, JSON, and XML — each has different use-cases and parsing/validation needs.
- Improper handling of headers or body data (unsanitised inputs, trusting Referer/User-Agent, insecure file uploads) leads to common web vulnerabilities.

### Explanation
**Request Headers**
  - Host — target domain (required for virtual hosts).
  - User-Agent — client/browser fingerprint; useful for analytics but untrusted for logic.
  - Referer — previous page URL; can be forged or omitted, never rely on it for auth.
  - Cookie — state/session data stored by the client; sensitive and must be protected (HttpOnly, Secure, SameSite).
  - Content-Type — describes format of the request body so the server knows how to parse it (e.g., application/json, multipart/form-data, application/x-www-form-urlencoded).
  - Headers are metadata — always treat values as untrusted input.
**Request Body**
  - application/x-www-form-urlencoded
  - Key=value pairs joined by &, percent-encoding for special characters.
  - Typical for simple form submissions.
  - body: name=Aleksandra&age=27&country=US.
**multipart/form-data**
  - Used for file uploads and mixed binary/text parts.
  - Boundaries separate parts; each part has its own headers (e.g., Content-Disposition, Content-Type).
  - Server must validate file type/size and handle binary safely.
**application/json**
  - JSON object structure: key: value pairs in {}.
  - Widely used for APIs.
  - Parse carefully and validate types/fields; beware of JSON-related injection if reflected.
**application/xml**
  - Tagged markup format with nested elements.
  - If accepted, protect against XXE (XML External Entity) and other XML-specific attacks.

### Notes
- Always validate and sanitize all header and body inputs on the server side — never trust client-sent values.
- Use the correct Content-Type and parse accordingly; mismatched types can cause parsing errors or vulnerabilities.
- For file uploads (multipart/form-data): validate file extension, MIME type, content, and impose size limits; store uploaded files outside web root or use safe renaming.
- Avoid placing sensitive data in URLs (GET query strings) — they can be logged or leaked. Use POST with secure transport (HTTPS) for confidential data.
- Apply security headers on responses (e.g., Content-Security-Policy, X-Frame-Options) and secure cookie flags (HttpOnly, Secure, SameSite).
- When building APIs, require explicit content negotiation and strict schema validation (e.g., JSON schema) to prevent malformed or malicious payloads.


## HTTP Response: Status Line and Status Codes

### Concepts Learned
- HTTP responses communicate the outcome of client requests using a Status Line and optional headers/body.
- Status Line contains three key parts: HTTP Version, Status Code, and Reason Phrase.
- Status Codes are grouped into categories: informational (100-199), success (200-299), redirection (300-399), client errors (400-499), server errors (500-599).
- Understanding status codes is essential for debugging, building web applications, and identifying potential attack responses (e.g., 404 vs 403).

### Explanation
**Status Line**
  - HTTP Version — protocol version (e.g., HTTP/1.1, HTTP/2).
  - Status Code — three-digit number indicating outcome (success, failure, redirection).
  - Reason Phrase — human-readable explanation of status code (e.g., “OK” for 200, “Not Found” for 404).
**Status Code Categories**
  - Informational (100-199): Request partially received; server expects more data (e.g., 100 Continue).
  - Successful (200-299): Request succeeded; server returns requested resource (e.g., 200 OK).
  - Redirection (300-399): Resource moved; client should request new location (e.g., 301 Moved Permanently).
  - Client Errors (400-499): Issues with the request (e.g., 404 Not Found, 403 Forbidden).
  - Server Errors (500-599): Server failed to process request (e.g., 500 Internal Server Error).
**Common Status Codes**
  - 100 Continue — server received partial request; continue sending.
  - 200 OK — request successful; server returning content.
  - 301 Moved Permanently — resource moved; use new URL.
  - 404 Not Found — requested resource unavailable.
  - 500 Internal Server Error — server-side error; request failed.

### Notes
- Status codes help distinguish between server-side vs client-side issues.
- Redirection codes require updating URLs in applications or browsers.
- Monitoring 4xx/5xx codes can help detect misconfigurations, broken links, or potential attack vectors.
- Always verify server responses during web development and security testing to handle errors gracefully.


## HTTP Response: Headers and Body

### Concepts Learned
- HTTP responses include headers and an optional body that deliver information about the request outcome and the content being returned.
- Response headers are key-value pairs that provide metadata and instructions to the client.
- Response body contains the actual content, such as HTML, JSON, or images.
- Proper handling of headers and body is essential for functionality, security, and performance of web applications.

### Explanation
**Response Headers**
  - Date — shows when the response was generated by the server.
  - Example: Date: Fri, 23 Aug 2024 10:43:21 GMT
  - Content-Type — indicates the type of content and charset.
  - Example: Content-Type: text/html; charset=utf-8
  - Server — identifies the server software (useful for debugging, can reveal info to attackers).
  - Example: Server: nginx
**Other Common Headers**
  - Set-Cookie — sets cookies on the client; use HttpOnly and Secure flags to protect session info.
  - Example: Set-Cookie: sessionId=38af1337es7a8
  - Cache-Control — controls caching behavior for responses.
  - Example: Cache-Control: max-age=600
  - Location — used for redirection; indicates new resource location.
  - Example: Location: /index.html
**Response Body**
  - Contains the actual data returned by the server (HTML, JSON, images, etc.).
  - Always sanitise and escape data, especially user-generated content, to prevent injection attacks like XSS.

### Notes
- Essential headers ensure proper response processing; optional headers provide control and security.
- Be cautious with sensitive headers like Server or Location to reduce attack surface.
- Proper sanitisation of the response body protects against XSS and other injection attacks.
- Monitoring headers and body content is important in both web development and penetration testing.


## HTTP Security Headers

### Concepts Learned
- Security headers enhance the protection of web applications by mitigating common attacks such as XSS, clickjacking, and information leakage.
**Common headers include:**
  - Content-Security-Policy (CSP)
  - Strict-Transport-Security (HSTS)
  - X-Content-Type-Options
  - Referrer-Policy
  - Tools like securityheaders.io can be used to analyze a website’s security headers.

### Explanation
**Content-Security-Policy (CSP)**
  - CSP helps prevent XSS by specifying which sources are allowed for content, scripts, and styles.
**Example:**
  - Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'
**Directives:**
  - default-src — sets default policy for all resources (e.g., 'self' allows only the same origin).
  - script-src — specifies allowed sources for scripts.
  - style-src — specifies allowed sources for CSS stylesheets.
**Strict-Transport-Security (HSTS)**
  - Ensures browsers always connect via HTTPS.
**Example:**
  - Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
**Directives:**
  - max-age — duration in seconds for enforcing HTTPS.
  - includeSubDomains — applies HSTS to all subdomains.
  - preload — adds site to browser preload lists to enforce HTTPS before the first visit.
**X-Content-Type-Options**
  - Prevents browsers from MIME-type sniffing, reducing certain attacks like XSS.
**Example:**
  - X-Content-Type-Options: nosniff
**Directive:**
  - nosniff — instructs the browser to strictly use the declared Content-Type without guessing.
**Referrer-Policy**
  - Controls the amount of referrer information sent when navigating between sites.
**Examples:**
  - Referrer-Policy: no-referrer
  - Referrer-Policy: same-origin
  - Referrer-Policy: strict-origin
  - Referrer-Policy: strict-origin-when-cross-origin
**Directives:**
  - no-referrer — disables sending referrer info completely.
  - same-origin — sends referrer only to the same origin.
  - strict-origin — sends only the origin when protocol is the same.
  - strict-origin-when-cross-origin — full URL sent for same-origin; origin only for cross-origin requests.

### Notes
- Implementing these headers improves web application security and reduces exposure to attacks.
- CSP is one of the most effective defenses against XSS and should be configured with care.
- HSTS should be used on all HTTPS websites to enforce secure connections.
- X-Content-Type-Options and Referrer-Policy provide additional layers of security and privacy.
- Regularly analyze your site with tools like securityheaders.io to ensure proper header configurations.


## Practical Task — Making HTTP Requests

### Concepts Learned
- HTTP methods (GET, POST, DELETE) perform distinct actions: retrieve, modify/create, and remove resources.
- REST endpoints map to resource operations (e.g., /api/users, /api/user/<id>).
- Server responses (status + body) confirm the outcome of requests and can return application-level messages or flags in lab environments.
- Using a web UI / Split View is sufficient to exercise and validate endpoint behaviour for basic REST interactions.

### Explanation
- GET /api/users: retrieves the list of users and any data the API exposes for that resource. Useful for discovery and confirming current server state.
- POST /api/user/2: updates the resource identified by /api/user/2 (in this task the country field for Bob). POST/PUT/PATCH are the typical methods used to change server-side data — always validate inputs and observe returned status/body.
- DELETE /api/user/1: removes the resource identified by /api/user/1. DELETE requests should be used with caution and confirmed by the server response.
- In the lab, the static site in Split View served as the API frontend — clicking through the UI and issuing the above requests let us confirm both the expected side effects and the server’s response messages.

### Notes (Hands‑On)
- Completed the GUI-based practical task using the Split View demo site.
**Verified and captured the lab responses/flags from the API after each request:**
  - GET /api/users → THM{YOU_HAVE_JUST_FOUND_THE_USER_LIST}
  - POST /api/user/2 (update Bob’s country UK → US) → THM{YOU_HAVE_MODIFIED_THE_USER_DATA}
  - DELETE /api/user/1 → THM{YOU_HAVE_JUST_DELETED_A_USER}
- Practical tip: when testing APIs in a browser-based demo, watch the response body/status and refresh state (re-run GET) to confirm changes persisted or were removed.


## Key Takeaways
- URLs define the location of resources on the web and consist of scheme, user info, host/domain, port, path, query string, and fragment — understanding these helps with navigation, development, and security.
- HTTP Messages are the foundation of web communication; requests and responses carry structured data through start lines, headers, and bodies.
- HTTP Requests use methods (GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS, TRACE, CONNECT) to interact with resources. Always validate inputs and control access.
- HTTP Responses include status lines, headers, and bodies; status codes indicate success, errors, or redirection. Headers convey metadata and control client behaviour.
- Request & Response Headers carry essential info for routing, content-type, authentication, cookies, caching, and security enforcement.
- HTTP Request/Response Bodies carry the actual data; formats like URL-encoded, multipart/form-data, JSON, and XML must be validated to prevent injection attacks.
- Security Headers (CSP, HSTS, X-Content-Type-Options, Referrer-Policy) add layers of protection against XSS, clickjacking, MIME sniffing, and information leakage.
- Hands-On API Practice reinforces understanding: GET retrieves, POST/PUT modifies, DELETE removes, and responses confirm the action.
- Always validate input, sanitize outputs, and review headers to improve security posture in web applications.
- Practical exercises help solidify theoretical knowledge by simulating real-world web interactions safely.
