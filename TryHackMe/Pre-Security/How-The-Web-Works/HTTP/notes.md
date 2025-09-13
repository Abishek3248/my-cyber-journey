# HTTP in Detail

## Introduction (HTTP, HTTPS)
- HTTP (HyperText Transfer Protocol) is the foundation of web browsing, created by Tim Berners-Lee between 1989–1991. It defines how web clients (like browsers) and servers communicate to transmit webpage data such as HTML, images, or videos.
- HTTPS (HyperText Transfer Protocol Secure) is the encrypted version of HTTP. It ensures confidentiality by encrypting traffic, prevents attackers from intercepting or tampering with data, and verifies the authenticity of the server through certificates.
- In the lab, I also explored the concept of invalid HTTP certificates, where a browser warns if the server’s certificate is misconfigured, expired, or issued by an untrusted authority.


## Requests and Responses

### Concepts Learned
- A URL specifies how and where to access resources on the internet.
- HTTP uses a request–response model between client and server.
- Requests include methods, paths, headers, and sometimes a body.
- Responses contain a status code, headers, and optional content.

### Explanation
- When accessing a website, the browser sends a request to the server, and the server replies with a response.
- Requests tell the server what resource is needed and include metadata in headers.
- Responses confirm success or failure using status codes, plus the resource content.

### Notes
 **URL Components**
- Scheme: Protocol (HTTP, HTTPS, FTP).
- User: Optional credentials (user:pass).
- Host: Domain name or IP of the server.
- Port: Connection port (default 80 for HTTP, 443 for HTTPS).
- Path: Location of the resource (e.g., /index.html).
- Query String: Extra info (e.g., ?id=1).
- Fragment: Reference to a section of the page (e.g., #task3).
 **Example Request**
    GET / HTTP/1.1
    Host: tryhackme.com
    User-Agent: Mozilla/5.0 Firefox/87.0
    Referer: https://tryhackme.com/
**Example Response**
    HTTP/1.1 200 OK
    Server: nginx/1.15.8
    Date: Fri, 09 Apr 2021 13:34:03 GMT
    Content-Type: text/html
    Content-Length: 98

## HTTP Methods

### Concepts Learned
- HTTP methods define the client’s intended action when making requests.
- Most common ones: GET, POST, PUT, DELETE.

### Explanation
- GET → Retrieve information from the server (e.g., load a webpage).
- POST → Send data to the server, often to create a new resource (e.g., submitting a form).
- PUT → Update existing information on the server.
- DELETE → Remove a resource or record from the server.

### Notes
- GET & POST are the most frequently used methods in web traffic.
- Methods help standardize communication between client and server.

## HTTP Status Codes

### Concepts Learned
- HTTP status codes indicate the outcome of a client’s request.
- They are categorized into 5 ranges: informational, success, redirection, client errors, server errors.
- Common status codes help interpret server responses quickly.

### Explanation
**HTTP Status Codes:**
- 100–199 (Informational) → Request accepted, continue sending (rarely used).
- 200–299 (Success) → Request completed successfully.
- 300–399 (Redirection) → Redirect client to another resource or URL.
- 400–499 (Client Errors) → Issue with the client’s request (e.g., missing parameters, unauthorized access).
- 500–599 (Server Errors) → Problem on the server side.
**Common HTTP Status Codes:**
- 200 OK → Request succeeded.
- 201 Created → New resource created.
- 301 Moved Permanently → Permanent redirect.
- 302 Found → Temporary redirect.
- 400 Bad Request → Request malformed or missing data.
- 401 Unauthorized → Authentication required.
- 403 Forbidden → No permission to access resource.
- 404 Not Found → Resource/page doesn’t exist.
- 405 Method Not Allowed → Incorrect HTTP method for the resource.
- 500 Internal Server Error → Server encountered an unexpected condition.
- 503 Service Unavailable → Server overloaded or down for maintenance.

### Notes
- Visual examples (like http.cat) help understand status codes quickly.
- Status codes can also be custom-defined by applications.


## Headers

### Concepts Learned
- Headers are extra information sent with HTTP requests and responses to facilitate proper communication between client and server.
- Request headers inform the server about the client and data being sent.
- esponse headers inform the client about the server, data type, and caching instructions.

### Explanation
 **Request Headers (Client → Server):**
- Host: Identifies which website on the server is being requested.
- ser-Agent: Browser type and version; helps server render content correctly.
- Content-Length: Indicates size of data being sent to the server.
- Accept-Encoding: Compression methods supported by the client.
- Cookie: Stores user-specific data for server-side reference.
 **Response Headers (Server → Client):**
- Set-Cookie: Stores data in client to send back on future requests.
- Cache-Control: Specifies how long content should be cached in the browser.
- Content-Type: Indicates the type of data (HTML, CSS, JS, images, etc.) so the client can process it correctly.
- Content-Encoding: Shows the compression method used to reduce data size during transmission.

### Notes
- Headers are optional, but most modern websites rely on them for proper display and functionality.
- Understanding headers helps in debugging, optimizing web performance, and security analysis.



## Cookies

### Concepts Learned:
- Cookies are small pieces of data stored on your computer by a web server.
- They track users, store preferences, or manage authentication sessions.
- Cookies are sent via the Set-Cookie header and included in future HTTP requests.

### Explanation:
- HTTP is stateless, so cookies allow websites to remember users between requests.
- Cookies usually store tokens or identifiers, not clear-text passwords.
- They are sent with every HTTP request to maintain session or preference information.
- Server Sends Cookie: When a user visits a website, the server sends a Set-Cookie header in the HTTP response.
- Browser Stores Cookie: The browser stores this cookie locally on the client device.
- Browser Sends Cookie: On every subsequent request to the same website, the browser automatically includes the cookie in the HTTP request header.
- Server Reads Cookie: The server reads the cookie to identify the user, maintain session, or customize responses.
- Cookie Updates / Expiration: Cookies may be updated by the server or expire after a set time defined by the Expires or Max-Age attribute.

### Notes:
- Use browser developer tools to view cookies:
- Open Developer Tools → Network Tab, select a request, then check the Cookies tab.
- Cookies persist on both client and server to manage sessions, user settings, or authentication.
- Understanding cookies helps in debugging, web development, and security testing.


## Practical

### Concepts Learned
- Practiced sending HTTP requests using GET, POST, PUT, and DELETE methods.
- Learned how to include URL parameters and body data in requests.
- Observed how servers respond to different HTTP methods.
- Understood practical applications of HTTP methods for resource retrieval, creation, updating, and deletion.

### Explanation
- GET Requests: Used to retrieve resources from the server. For example, retrieving the blog page with a specific ID to see its content.
- POST Requests: Used to send data to the server, such as logging in with a username and password.
- PUT Requests: Used to update existing resources, like modifying a user’s information on the server.
- DELETE Requests: Used to remove resources, such as deleting a user record.
- URL parameters and request body fields determine what specific data is retrieved or modified on the server.

### Notes
- Used a beginner-friendly GUI environment where input automatically typed into a terminal for demonstration.
- Sent a GET request to the room page to access its content.
- Accessed a blog page using GET with a query parameter to view a specific blog post.
- Updated user data by sending a PUT request with the new username.
- Deleted a user record using a DELETE request.
- Logged in to the server using a POST request with username and password.


## Key Takeaways
- HTTP is the core protocol for transferring web resources, with HTTPS providing secure, encrypted communication.
- URLs define how and where to access resources, specifying scheme, host, port, path, query parameters, and fragments.
- HTTP requests use methods like GET, POST, PUT, and DELETE to interact with server resources.
- Responses include status codes indicating success, redirection, client errors, or server errors.
- Headers provide additional context for requests and responses, including content type, length, and caching instructions.
- Cookies allow servers to store stateful information on the client, enabling authentication and personalization.
- Practical HTTP exercises reinforce understanding of request formation, parameter usage, and server responses.
