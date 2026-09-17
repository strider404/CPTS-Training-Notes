
2025-07-29 09:44

Tags: #web  

## HyperText Transfer Protocol (HTTP)

- **Definition**: HTTP is an *application-level protocol* used for communications on the internet, enabling access to World Wide Web resources. It operates on a *client-server model.*
  
- **Process**: A client (e.g., a web browser) sends a request to a server for a specific resource. The server processes this request and returns the resource in a response.
  
- **Port**: The default communication port for HTTP is **port 80**, although this can be configured differently on the web server.
  
## URL (Uniform Resource Locator) Structure

![[Pasted image 20250729094714.png]]

- A URL is used to **specify and access resources**. Its components are:
	- **Scheme**: The protocol being used, ending in `://` (e.g., `http://`).
    
	- **User Info**: Optional authentication credentials (`username:password@`).
    
	- **Host**: The location of the resource, which can be a domain name or an IP address (e.g., `www.hackthebox.com`).
    
	- **Port**: The specific port on the host, separated by a colon (e.g., `:80`). If omitted, it defaults to port 80 for `http` and 443 for `https`.
    
	- **Path**: The specific resource being accessed on the server (e.g., `/dashboard.php`).
    
	- **Query String**: Starts with `?` and contains parameters as key-value pairs (e.g., `?id=1`). Multiple parameters are separated by `&`.
    
	- **Fragments**: Starts with `#` and points to a specific section within the page, processed client-side by the browser.


- Schema and Host are **mandatory**


## HTTP Flow

![[Pasted image 20250729095252.png]]

- **DNS Resolution**: A user enters a URL. The browser first queries a Domain Name System (DNS) server to resolve the domain name into an IP address. It may check the local `/etc/hosts` file first.
  
- **Request**: Using the obtained IP address, the browser sends an HTTP `GET` request to the server's default port (e.g., 80), typically asking for the root path (`/`).
  
- **Server Processing**: The web server receives and processes the request. By default, it returns a default file like `index.html` for a root path request.
  
- **Response**: The server sends back an HTTP response containing the requested resource and a status code (e.g., `200 OK` for success).
  
- **Rendering**: The browser receives the response and renders the content (e.g., HTML, CSS, JavaScript) for the user.


## cURL (Client URL)

- **Purpose**: `cURL` is a command-line tool for *transferring data with URLs*, supporting HTTP and many other protocols. It is critical for scripting and web penetration testing.

- **Function**: It *sends requests* and *prints the raw response* from the server to the terminal, rather than rendering it like a browser.

- - **Common Flags**:
    - `curl <url>`: Makes a basic request.
      
    - `-O`: Saves the output to a file named after the remote file.
      
    - `-o <file>`: Saves the output to a specified file name.
      
    - `-s`: Activates silent mode, hiding progress and error messages.
      
    - `-h`: Displays a summary of options. `man curl` provides the full manual.
## References:

https://academy.hackthebox.com/module/35/section/219