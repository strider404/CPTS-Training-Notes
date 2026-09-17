
2025-07-25 10:10

Tags: #web  
## Web Servers

- A **web server** is a back-end application that **processes incoming HTTP(S) requests** from clients (e.g., web browsers), and **sends responses back** to the client's browser.

- Its primary responsibilities include **routing requests** to the appropriate resource, **executing necessary processes**, and **returning an HTTP response.**

- Web servers typically operate on **TCP port 80** for HTTP and **port 443** for HTTPS.

## Workflow

![[Pasted image 20250725101824.png]]

- **Request Handling:** A web server accepts various types of user input within HTTP requests, such as text, JSON, and binary data for file uploads.

- **Response Generation:** It sends back an **HTTP response**, which contains a **status code** and, if successful, the requested content.

- **HTTP Status Codes:** These codes communicate the result of the request. Common categories include ([all here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)):
	- **Successful (2xx):** e.g., `200 OK` indicates the request succeeded.
	  
	- **Redirection (3xx):** e.g., `301 Moved Permanently` indicates the resource URL has changed.
	  
	- **Client Error (4xx):** e.g., `404 Not Found` when a resource doesn't exist or `403 Forbidden` for unauthorized access attempts.
	  
	- **Server Error (5xx):** e.g., `500 Internal Server Error` when the server encounters an unexpected condition.

#### Common Web Server Software

- **Apache HTTP Server (`httpd`):**
	- Reportedly the most common web server, powering over 40% of websites.
	  
	- It is open-source, well-documented, and highly extensible via modules.
	  
	- Frequently used with **PHP**, but it also supports other languages like Python and Perl through CGI.


- **NGINX:**
	- The second most common server, noted for its use in approximately 30% of all websites and 60% of the top 100,000 high-traffic sites.
	  
	- Its asynchronous architecture is optimized for high concurrency with low memory and CPU usage, making it highly reliable for popular applications.
	  
	- It is also free and open-source.

- **Microsoft Internet Information Services (IIS):**
	- The third most common server, hosting about 15% of websites.
	  
	- Developed by Microsoft and runs on Windows Server environments.
	  
	- Primarily used for hosting applications built on the **Microsoft .NET framework** and integrates well with **Active Directory**.

## References:
https://academy.hackthebox.com/module/75/section/760
