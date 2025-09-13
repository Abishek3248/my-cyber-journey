# Cheatsheet – HTTP in Detail

## HTTP Methods

| Method | Description                                      | Common Use Case                   |
|--------|-------------------------------------------------|----------------------------------|
| GET    | Retrieves data from the server                  | Loading webpages, fetching data  |
| POST   | Submits data to the server, can create records | Forms, login credentials         |
| PUT    | Updates existing data on the server            | Editing user profiles, updating posts |
| DELETE | Removes resources from the server              | Deleting users or content        |

---

## HTTP Status Codes

| Code Range | Meaning                 | Example / Notes                                     |
|------------|------------------------|----------------------------------------------------|
| 100–199    | Informational          | Continue sending request (rarely used)            |
| 200–299    | Success                | 200 OK – request succeeded, 201 Created – new resource |
| 300–399    | Redirection            | 301 Moved Permanently, 302 Found                  |
| 400–499    | Client Errors          | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found |
| 500–599    | Server Errors          | 500 Internal Server Error, 503 Service Unavailable |

---

## HTTP Headers

### Common Request Headers

| Header           | Purpose                                                                 |
|-----------------|-------------------------------------------------------------------------|
| Host             | Specifies which website on a server to access                           |
| User-Agent       | Browser or client software info                                         |
| Content-Length   | Size of data being sent to server                                       |
| Accept-Encoding  | Supported compression formats                                           |
| Cookie           | Sends previously stored cookies to server                               |

### Common Response Headers

| Header           | Purpose                                                                 |
|-----------------|-------------------------------------------------------------------------|
| Set-Cookie       | Stores cookies on client                                               |
| Cache-Control    | Specifies how long content should be cached                             |
| Content-Type     | Indicates type of returned data (HTML, CSS, JSON, etc.)                 |
| Content-Encoding | Method used to compress data                                            |

---

## URLs

| Component       | Purpose / Description                                                  | Example                                     |
|----------------|------------------------------------------------------------------------|---------------------------------------------|
| Scheme          | Protocol to use (http, https, ftp)                                     | http://                                    |
| User            | Optional username/password for authentication                           | user:pass@                                  |
| Host            | Domain or IP address of server                                         | tryhackme.com                               |
| Port            | Network port to connect to (default: 80 HTTP, 443 HTTPS)              | :80                                         |
| Path            | Resource or file location on server                                     | /blog                                        |
| Query           | Parameters to pass to resource                                         | ?id=1                                       |
| Fragment        | Direct reference to section in page                                    | #section                                    |

---

## Cookies

| Concept             | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| Set-Cookie Header   | Sent by server to store state/data on client                            |
| Cookie Transmission | Browser sends stored cookies back with every request                   |
| Common Uses         | Authentication, personalization, session tracking                     |
| Viewing Cookies      | Use browser Developer Tools → Network tab → Cookies                     |

---

## Quick Practical Tips

| Action                                | Example / Notes                                    |
|--------------------------------------|---------------------------------------------------|
| GET request to fetch webpage          | GET /blog?id=1                                   |
| POST request to send data             | POST /login with username/password               |
| PUT request to update resource        | PUT /user/2 with JSON body                       |
| DELETE request to remove resource     | DELETE /user/1                                   |
| Inspect request/response headers      | Browser Developer Tools → Network tab            |
| Test status codes visually            | http.cat or browser response                      |


