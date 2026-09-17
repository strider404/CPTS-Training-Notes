
2025-09-12 15:11

Tags: #footprint  

## Remote Desktop Protocol (RDP)

- **Purpose:** Provides remote access to a Windows computer's **graphical user interface (GUI).**

- Typically uses **TCP port 3389**.

- Requires **firewall rules** and potentially port forwarding through NAT to be accessible.

- **Security:**
	- Uses Transport Layer Security (TLS/SSL) for encryption.
	  
	- A common vulnerability is the **default use of self-signed certificates**, which makes it difficult for a client to verify the server's identity.
	  
	- **Network Level Authentication (NLA)** is a default security feature to enhance protection.

#### Footprinting

- **Nmap:** Can be used to scan port 3389 to discover the server version, hostname, and whether NLA is enabled. Note that Nmap's default RDP scripts use a specific cookie (`mstshash=nmap`) that can be detected by security systems like EDR.
	- ![[Pasted image 20250912153549.png]]

- **rdp-sec-check.pl:** A Perl script from Cisco that can **check the security configurations** (supported protocols and encryption levels) of an RDP server.
	- [Github](https://github.com/CiscoCXSecurity/rdp-sec-check)
	- ![[Pasted image 20250912153939.png]]

- **Clients:** On Linux, tools like `xfreerdp`, `rdesktop`, and `Remmina` can be used to connect to an RDP server.
	- ![[Pasted image 20250912154006.png]]


## Windows Remote Management (WinRM)

- **Purpose:** A **command-line based protocol** for remote management and command execution.

- - **Technical Details:**
    - Uses the Simple Object Access Protocol (SOAP).
      
    - Listens on **TCP port 5985 (HTTP)** and **TCP port 5986 (HTTPS)**.
      
    - Works with Windows Remote Shell (WinRS) to execute commands.
      
    - It is a requirement for features like PowerShell Remoting.


- **Footprinting and Interaction:**
	- **Nmap:** Can scan ports 5985 and 5986 to identify the service.
	  
	- **PowerShell:** The `Test-WsMan` cmdlet can check if a host is reachable via WinRM.
	  
	- **Evil-WinRM:** A tool used on Linux to interact with WinRM for penetration testing.
		- ![[Pasted image 20250912154143.png]]


## Windows Management Instrumentation (WMI)

- **Purpose:** Microsoft's implementation of the Web-Based Enterprise Management (WBEM) standard, allowing **deep read and write access** to nearly all **Windows system settings**.

- **Technical Details:**
	- The initial connection always occurs on **TCP port 135**.
	- After the initial handshake, communication is transferred to a random, high-numbered port.

- **Footprinting and Interaction:**
	- **Impacket:** The `wmiexec.py` script from the **Impacket** toolkit can be used to execute commands on a remote system via WMI.
	- ![[Pasted image 20250912154302.png]]


## References:
https://academy.hackthebox.com/module/112/section/1242
