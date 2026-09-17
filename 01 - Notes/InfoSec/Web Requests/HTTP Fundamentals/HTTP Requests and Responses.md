
2025-07-29 10:29

Tags: #web  

## HTTP Requests and Responses

- A client, such as a web browser or cURL, initiates an **HTTP Request** to a server to ask for a resource.

- The server processes this request and sends back an **HTTP Response**.

- The response includes a **status code** and, if successful and applicable, the requested **resource** data.

## HTTP Request

![[Pasted image 20250729103219.png]]

- **Start-Line**: Comprises three space-separated fields:
	- **Method**: The type of action, e.g., `GET`.
	  
	- **Path**: The resource location, e.g., `/users/login.html`.
	  
	- **Version**: The protocol version, e.g., `HTTP/1.1`.

- **Headers**: *Key-value pairs* that specify request attributes, such as `Host`, `User-Agent`, and `Cookie`.

- **Body** (Optional): Contains data sent to the server.
  
- **Protocol Versions**: HTTP/1.x transmits requests as clear text, whereas HTTP/2.x uses a binary data format.

## HTTP Response

![[Pasted image 20250729103505.png]]

- **Status-Line**: Contains two primary fields:
	- **Version**: The protocol version, e.g., `HTTP/1.1`.
	  
	- **Status Code**: Indicates the result of the request, e.g., `200 OK` or `401 Unauthorized`.

- **Headers**: Key-value pairs sent by the server, such as `Date`, `Content-Length`, and `Content-Type`.

- **Body** (Optional): The content returned by the server, which can be HTML, JSON, images, scripts, or documents.

## Tools for HTTP Inspection

- **cURL**:
	- A command-line tool for transferring data with URLs.
    
	- The `-v` (verbose) flag allows you to view the **full HTTP request and response,** which is useful for penetration testing.

- **Browser Developer Tools (DevTools)**:
	- Integrated tools in modern browsers, accessible via `CTRL+SHIFT+I` or `F12`.
	  
	- The **Network** tab is particularly useful as it logs all network activity, allowing inspection of individual request and response details like status, method, and domain.

## References:

https://academy.hackthebox.com/module/35/section/220