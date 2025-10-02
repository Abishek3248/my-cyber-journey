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


# Examples

| Category | Type / Method | Example |
|----------|---------------|---------|
| **HTTP Methods** | GET | `GET /api/users HTTP/1.1` |
| | POST | `POST /api/user HTTP/1.1` + JSON body |
| | PUT | `PUT /api/user/2 HTTP/1.1` + JSON body |
| | DELETE | `DELETE /api/user/1 HTTP/1.1` |
| **Request Headers** | Host | `Host: tryhackme.com` |
| | User-Agent | `User-Agent: Mozilla/5.0` |
| | Content-Type | `Content-Type: application/json` |
| | Cookie | `Cookie: sessionId=abc123` |
| **Request Body Types** | URL-Encoded | `name=Alice&age=25` |
| | Form Data | Multipart upload: `username=Alice`, `file=photo.jpg` |
| | JSON | `{ "name": "Alice", "age": 25 }` |
| | XML | `<user><name>Alice</name><age>25</age></user>` |
| **Response Status Codes** | Success | `200 OK` |
| | Redirect | `301 Moved Permanently` |
| | Client Error | `404 Not Found` |
| | Server Error | `500 Internal Server Error` |
| **Security Headers** | CSP | `Content-Security-Policy: default-src 'self'` |
| | HSTS | `Strict-Transport-Security: max-age=63072000; includeSubDomains` |
| | X-Content-Type-Options | `nosniff` |
| | Referrer-Policy | `strict-origin-when-cross-origin` |
