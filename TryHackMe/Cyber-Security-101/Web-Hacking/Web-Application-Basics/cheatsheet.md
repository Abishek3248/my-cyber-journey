# Cheatsheet - Web Application Basics
 
| Topic | Key Points | Examples / Notes |
|-------|------------|-----------------|
| **URL** | Uniform Resource Locator, identifies resource location | `https://example.com:443/path?query=1#section` |
| **URL Components** | Scheme, User, Host/Domain, Port, Path, Query, Fragment | Scheme: `https`, Port: `443`, Path: `/api/users` |
| **HTTP Request** | Start line (Method, Path, Version), Headers, Body | Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS, TRACE, CONNECT |
| **HTTP Methods** | GET: fetch, POST: create/update, PUT: replace, DELETE: remove | Validate inputs & control access |
| **Request Headers** | Provide extra info, control behavior | `Host`, `User-Agent`, `Referer`, `Cookie`, `Content-Type` |
| **Request Body** | Data sent to server | Formats: URL-encoded, JSON, XML, multipart/form-data |
| **HTTP Response** | Status line, headers, body | Status codes: 200 OK, 404 Not Found, 500 Internal Server Error |
| **Response Headers** | Provide response metadata | `Content-Type`, `Date`, `Server`, `Set-Cookie`, `Cache-Control`, `Location` |
| **Security Headers** | Mitigate attacks like XSS, clickjacking, info leakage | `CSP`, `HSTS`, `X-Content-Type-Options: nosniff`, `Referrer-Policy` |
| **HTTP Versions** | Protocol used between client and server | HTTP/1.1, HTTP/2, HTTP/3 |
| **Key Security Tips** | Input validation, output sanitization, secure headers, HTTPS enforcement | Prevent injection, XSS, open redirects, info leaks |
| **Practical API Requests** | GET: read, POST/PUT: modify, DELETE: remove | Check flags/responses in lab exercises (e.g., THM labs) |
