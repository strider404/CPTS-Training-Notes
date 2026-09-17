
2025-09-08 09:57

Tags: #footprint  

## SMTP

- **SMTP (Simple Mail Transfer Protocol)** is a client-server protocol used for *sending emails* across IP networks. It can operate between an email client and a mail server or between two mail servers.

-  **Email Flow Components:**
	- **MUA (Mail User Agent):** The email client used by the end-user.
	  
	- **MSA (Mail Submission Agent)/Relay Server:** Receives email from the MUA and validates it before passing it on.
	  
	- **MTA (Mail Transfer Agent):** The core software that sends email to and receives email from other MTAs.
	  
	- **MDA (Mail Delivery Agent):** Delivers the final email to the recipient's mailbox for retrieval via POP3/IMAP.


- **Operating Ports:**
	- **Port 25:** The *default* port, traditionally for *unencrypted* communication.
	  
	- **Port 587:** A *newer* standard port for email submission, typically requiring authentication and using `STARTTLS` to upgrade the connection to be encrypted.
	  
	- **Port 465:** An older port used for connections that are encrypted with *SSL/TLS* from the start.


- **Inherent Security Weaknesses:**
	- **Lack of Encryption:** By default, SMTP transmits all data, including credentials, in plaintext.
	  
	- **No Sender Authentication:** The base protocol does not verify the sender's identity, which enables email spoofing and spam.
	  
	- **Unreliable Delivery Confirmation:** Delivery failure notifications are not standardized and often unhelpful.


- **Default Configuration**
	- In `/etc/postfix/main.cf`
  
- **Commands**
![[Pasted image 20250908100714.png]]


- [SMTP responses](https://serversmtp.com/smtp-error/)


- Using *telnet* or *netcat* to connect


- **Security Enhancements (ESMTP):**
	- **ESMTP (Extended SMTP):** Modern implementations of SMTP that include extensions for security.
	  
	- **Encryption:** The `STARTTLS` command is used to upgrade a plaintext connection to an encrypted one using TLS.
	  
	- **Authentication:** `SMTP-AUTH` is an extension that requires the client to authenticate with a username and password.
	  
	- **Anti-Spoofing:** Mechanisms like **SPF** (Sender Policy Framework) and **DKIM** (DomainKeys Identified Mail) are used to verify the sender's domain.


## Footprinting

- Default Nmap script (`-sC`) contains `smtp-commands`, which uses the `EHLO` command to list all possible commands that can be executed on the target SMTP server.
	- ![[Pasted image 20250908164134.png]]


- **Major Vulnerability: Open Relay:**
	- An SMTP server is an **"open relay"** if it is misconfigured to *accept and forward email from any user to any destination*, without authentication.
	  
	- This is a critical vulnerability often exploited to *send large volumes of spam and malicious emails.*

- Tools like **Nmap** have scripts (`smtp-open-relay`) to test for this misconfiguration.
![[Pasted image 20250908102047.png]]



- **smtp-user-enum** can be used to automatically check users in that SMTP server based on a wordlist
	- Remember to increase the `-w` if there are too many "no result"
	- ![[Pasted image 20250908164028.png]]

## References:
https://academy.hackthebox.com/module/112/section/1072
