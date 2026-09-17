
2025-07-29 11:10

Tags: #web  

## HTTP Basic Auth

- This is a **simple authentication scheme** handled directly *by the web server* to protect a page or directory, separate from the web application's logic.

- When accessing a protected resource **without credentials**, the server responds with a `401 Authorization Required` status and a `WWW-Authenticate: Basic` header.
	- ![[Pasted image 20250729113220.png]]

- **Credentials can be supplied in several ways:**
	- Through the browser prompt.
    
	- Using `curl` with the `-u username:password` flag.
    
	- Embedding credentials directly in the URL: `http://username:password@<SERVER_IP>:<PORT>/` (can also be used with curl)

## HTTP Authorization Header

- When using Basic Authentication, the client sends an **Authorization header** with the request.
	- ![[Pasted image 20250729113919.png]]

- The header's value is structured as `Basic <credentials>`, where `<credentials>` is the **Base64** encoded string of `username:password`.
	- For example, `admin:admin` becomes `YWRtaW46YWRtaW4=`.

- You can manually add this header to a `curl` request using the `-H` flag (e.g., `curl -H 'Authorization: Basic YWRtaW46YWRtaW4='`). (another way to access credential-required pages)

## GET Parameters

- Data can be passed to the server within the URL of a GET request, known as **URL parameters** (e.g., `/search.php?search=le`).
	- ![[Pasted image 20250729114948.png]]

- The browser's **Network tab** can be used to identify these requests and their parameters.

- Developer tools offer convenient features to replicate these requests for analysis:
	- **Copy as cURL**: Generates a complete `curl` command to replicate the request in a terminal.
	  
	- **Copy as Fetch**: Generates JavaScript code using the `Fetch` API to replicate the request in the browser's console.

## References:
https://academy.hackthebox.com/module/35/section/247