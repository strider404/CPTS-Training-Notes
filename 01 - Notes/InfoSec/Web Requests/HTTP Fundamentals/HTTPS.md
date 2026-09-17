
2025-07-29 10:04

Tags: #web  

## Hypertext Transfer Protocol Secure (HTTPS)

- **Fundamental Problem with HTTP**: The Hypertext Transfer Protocol (HTTP) transmits data in **clear-text**, rendering it susceptible to Man-in-the-Middle (MiTM) attacks where an attacker can intercept and read sensitive information, such as login credentials.
	- ![[Pasted image 20250729100650.png]]

- **HTTPS as the Solution**: HTTPS (HTTP Secure) resolves this vulnerability by **encrypting all communication** between the client (web browser) and the server. Even if traffic is intercepted, the data remains a single, unreadable encrypted stream. Consequently, HTTPS is becoming the web standard, with browsers phasing out support for insecure HTTP connections.
	- ![[Pasted image 20250729100806.png]]

## HTTPS Flow

![[Pasted image 20250729101751.png]]

- If a user attempts to access a secure site using `http://` (port 80), the server issues a `301 Moved Permanently` response, **redirecting the client to the secure HTTPS port 443.**
  
- The client initiates a "client hello" packet.
  
- The server responds with a "server hello" and its **SSL certificate** for key exchange.
  
- The client verifies the server's certificate and may send its own.
  
- An encrypted handshake is performed to confirm the integrity of the secure connection.
  
- Once the handshake is complete, all subsequent HTTP communication is encrypted.

- **Potential Vulnerabilities**:
	- **DNS Leakage**: Although the data is encrypted, the domain name being accessed may still be revealed if the request goes through an **unencrypted DNS server.** The use of encrypted DNS (e.g., `8.8.8.8`, `1.1.1.1`) or a VPN is recommended to mitigate this.
	  
	- **Downgrade Attacks**: An attacker could potentially perform a MiTM attack to force a connection to *downgrade from HTTPS to HTTP*. However, most modern browsers and servers have countermeasures to prevent this.

## cURL for HTTPS

- The `cURL` command-line tool automatically handles the HTTPS handshake and encryption.
  
- By default, `cURL` will *refuse to connect to a server with an invalid or outdated SSL certificate* to protect against MiTM attacks.

- For testing purposes (e.g., a local application without a valid certificate), the `-k` or `--insecure` flag can be used to instruct `cURL` to bypass the certificate validation and proceed with the connection.
## References:
https://academy.hackthebox.com/module/35/section/228
