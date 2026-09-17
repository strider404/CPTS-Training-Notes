
2025-09-09 11:24

Tags: #footprint  

## IMAP - POP3

- **IMAP (Internet Message Access Protocol):** Allows for the *online management of emails directly on a remote server.* It functions like a network file system for emails, supporting folder structures and synchronization across multiple clients. Emails remain on the server until deleted.

- **POP3 (Post Office Protocol):** Provides *more limited functionality*, typically restricted to listing, retrieving (often downloading to a single client), and deleting emails from the server. It lacks the advanced management and synchronization features of IMAP.


- **Protocol Type:** IMAP is a *text-based, client-server* protocol using ASCII commands.


- **Connection Ports:**
	- **IMAP:** Port **143** (unencrypted)
	  
	- **IMAPS (IMAP over SSL/TLS):** Port **993** (encrypted)
	  
	- **POP3:** Port **110** (unencrypted)
	  
	- **POP3S (POP3 over SSL/TLS):** Port **995** (encrypted)


- **Operation:** A client connects, authenticates with a username and password, and then sends commands to manage mailboxes. It supports simultaneous access by multiple users and can offer offline functionality by synchronizing a local copy.


- **IMAP commands:**
![[Pasted image 20250909112928.png]]

- [FULL COMMANDS](https://www.atmail.com/blog/imap-commands/)
- To read an email in a mailbox, first `SELECT`, then `SEARCH` to find the IDs, then `FETCH` (pay attention to the **FETCH options** in the above link)


- **POP3 commands:**
![[Pasted image 20250909112945.png]]


#### Security Concerns and Vulnerabilities

- **Encryption:** By default, IMAP and POP3 are *unencrypted*, transmitting credentials and emails in plain text. SSL/TLS is required to secure the communication channel.

- **Dangerous Configurations:** Server-side misconfigurations can lead to serious vulnerabilities. Examples include:
	- `auth_debug` and `auth_debug_passwords`: These settings can log authentication attempts, including passwords, in plain text.
	- `auth_anonymous_username`: This may allow for anonymous, unauthenticated access.


- **Information Disclosure:** Misconfigurations can allow an attacker to read, send, or delete emails, potentially exposing confidential information.

## Footprinting

- **Scanning:** Tools like **Nmap** are used to discover open IMAP/POP3 ports, identify service versions, and inspect SSL certificates for information like organization name and domain.


- **Interaction:** Tools such as **cURL**, **OpenSSL**, and **ncat** can be used to connect to the server, test credentials, and manually issue commands to interact with the mail service.
	- **cURL**
	- ![[Pasted image 20250909113217.png]]
	- **OpenSSL**
	- ![[Pasted image 20250909113234.png]]
	- ![[Pasted image 20250909113242.png]]
## References:

https://academy.hackthebox.com/module/112/section/1073