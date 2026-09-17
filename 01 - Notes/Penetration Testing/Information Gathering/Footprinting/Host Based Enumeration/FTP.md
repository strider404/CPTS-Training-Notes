
2025-09-04 10:25

Tags: #footprint  

## FTP

- **Definition**: FTP is an *application-layer protocol* used for transferring files between a client and a server.

- [Last FTP assessment](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FNetwork%20Foundations%2FSkills%20Assessment)

- **Mechanism**
	- It establishes *two* separate TCP connections.
    
	- **Control Channel (Port 21)**: Used for sending commands (from client) and status codes (from server).
    
	- **Data Channel (Port 20)**: Used exclusively for the actual file transfer.
    
	- It supports resuming interrupted transfers.


- **Modes**
	- **Active Mode**: The client informs the server of a port (in client's side) to connect back to for data transfer. This can be *blocked by firewalls on the client's side.*
    
	- **Passive Mode**: The server *provides a port* for the client to connect to for data transfer. This is more firewall-friendly as the client initiates all connections.


- **Security**
	- FTP is a **clear-text protocol**, meaning credentials and data are sent unencrypted and are vulnerable to sniffing.
    
	- **Anonymous FTP** is an option where servers allow access without credentials, though typically with restricted permissions.


## Trivial File Transfer Protocol (TFTP)

- **Definition**: TFTP is a simplified version of FTP.

- **Key Differences from FTP**:
	- It uses **UDP** instead of TCP, making it an unreliable protocol.
	  
	- It provides **no user authentication** (no passwords).
	  
	- It lacks advanced features like directory listing.

- **Use Case**: Due to its lack of security, TFTP should only be used in secure, local networks.


## vsFTPd (Very Secure FTP Daemon)

- **Definition**: A popular and common *FTP server* software for Linux systems.


- **Configuration**:
	- The main configuration file is located at `/etc/vsftpd.conf`.
		- ![[Pasted image 20250904110118.png]]
		  
	- The `/etc/ftpusers` file lists users who are explicitly denied access to the FTP service.
		- ![[Pasted image 20250904110204.png]]


## Dangerous Settings

- ![[Pasted image 20250904111420.png]]

#### Anonymous Login

- IF the first option is enable, allowing `anonymous` access
![[Pasted image 20250904111537.png]]


#### Download a File


![[Pasted image 20250904111739.png]]

- **Download All Available Files**

![[Pasted image 20250904111807.png]]


#### Upload a File

![[Pasted image 20250904111833.png]]


- **Note**:  Always use the Ctrl + V + Enter + Enter
## Footprinting the Service

- **Initial Connection**: When connecting, an FTP server often presents a **banner** that can reveal the software name and version (e.g., `vsFTPd 3.0.3`), which is critical information for an attacker.


- **File System Enumeration**:
	- The `ls -R` command, if enabled on the server (`ls_recurse_enable=YES`), can recursively list all files and directories, providing a complete map of the accessible data.


- **Nmap Scanning**:
	- The **Nmap Scripting Engine (NSE)** has scripts specifically for FTP, such as:
	    - `ftp-anon`: Checks if anonymous login is permitted and lists the contents.
	      
	    - `ftp-syst`: Retrieves system status and version information from the server.


- **Service Interaction**:
	- Utilities like `netcat` and `telnet` can be used for manual, low-level interaction with the FTP service.
		- ![[Pasted image 20250904112053.png]]
		  
	- For encrypted connections (FTP over TLS/SSL), `openssl s_client` can be used. This tool can also inspect the server's SSL certificate, potentially revealing hostnames, organizational details, and email addresses.
## References:

https://academy.hackthebox.com/module/112/section/1066