
2025-08-06 10:15

Tags:  

## Workflow

- ![[Pasted image 20250806105305.png]]

- **Pre-Engagement**
	- **Description**: This is the initial planning phase where the *scope, tasks, and legal agreements* are established with the client.


- **Information Gathering**
	- **Description**: After building a foundation, this stage focuses on *actively enumerating* identified targets to *find* specific details and potential attack vectors.
	  
	- **Recommended Modules**:
		- Network Enumeration with Nmap
		  
		- Footprinting
		  
		- Information Gathering - Web Edition
		  
		- OSINT: Corporate Recon


- **Vulnerability Assessment**
	- **Description**: In this stage, you *analyze* the gathered information to *identify potential weaknesses*, using both automated scanners and manual analysis.
	  
	- **Recommended Modules**:
		- Vulnerability Assessment
		  
		- File Transfers
		  
		- Shells & Payloads
		  
		- Using the Metasploit-Framework

- **Exploitation**
	- **Description**: This is the *active attack phase* where you attempt to exploit discovered vulnerabilities to gain access. It is broken into two key areas: general services and web applications.
	  
	- **Recommended General Exploitation Modules**:
	    - Password Attacks
        
	    - Attacking Common Services
        
	    - Pivoting, Tunneling & Port Forwarding
        
	    - Active Directory Enumeration & Attacks
    
	- **Recommended Web Exploitation Modules**:
	    - Using Web Proxies
        
	    - Attacking Web Applications with Ffuf
        
	    - Login Brute Forcing
        
	    - SQL Injection Fundamentals & SQLMap Essentials
        
	    - Cross-Site Scripting (XSS)
        
	    - File Inclusion
        
	    - Command Injections
        
	    - Advanced Web Attacks
        
	    - Attacking Common Applications


- **Post-Exploitation**
	- **Description**: After gaining initial access, the goal is often to *escalate privileges* to gain more control over the compromised system.
	  
	- **Recommended Modules**:
		- Linux Privilege Escalation
		  
		- Windows Privilege Escalation

- **Lateral Movement**
	- **Description**: This involves using a compromised host to *move through the network* and attack other internal systems. Techniques for this are integrated within various modules, such as the privilege escalation modules.

- **Proof-of-Concept (POC)**
	- **Description**: This phase involves creating a demonstration (e.g., a script) that proves the existence of a vulnerability for the client's technical team to reproduce.
	  
	- **Recommended Module**:
	    - Introduction to Python 3

- **Post-Engagement**
	- **Description**: The final stage involves cleaning up any tools or files from the client's systems and delivering a comprehensive, high-quality penetration test report.
	  
	- **Recommended Modules**:
	    - Documentation & Reporting
	      
	    - Attacking Enterprise Networks


## References:

https://academy.hackthebox.com/module/90/section/1559