
2025-09-03 10:04

Tags: #footprint  

## Information Gathering Workflow

- **Initial Website Analysis**
	- Begin by thoroughly *examining the company's main website.*
    
	- Identify the services offered (e.g., app development, hosting, IoT) to infer the technologies and infrastructure required to support them.



- **Discovering Online Presence & Subdomains**
	- **SSL/TLS Certificates:** Inspect the main *website's certificate*, as it often includes other subdomains it is valid for.
		- ![[Pasted image 20250903102456.png]]
    
	- **Certificate Transparency Logs:** Use services like **`crt.sh`** to search public logs of all issued certificates for a domain. This is a primary method for discovering subdomains (e.g., `matomo.inlanefreight.com`, `shop.inlanefreight.com`).
		- ![[Pasted image 20250903102843.png]]



- **Identifying In-Scope Assets**
	- Use commands like **`host`** to resolve discovered subdomains to IP addresses.
		- ![[Pasted image 20250903154745.png]]
    
	- Filter out assets hosted by third-party providers (unless they are explicitly in scope) to focus on servers managed directly by the target company.


- **Scanning with Shodan**
	- Use the list of identified, company-hosted IP addresses to query **Shodan**.
    
	- Shodan reveals information about internet-connected devices, including open TCP/IP ports, running services (e.g., `nginx`, `OpenSSH`, `Apache`), and service versions.


- **Analyzing DNS Records**
	- se a tool like **`dig`** to query for all available DNS records for the domain.
    
	- **`A` records:** Map domains to IP addresses.
    
	- **`MX` records:** Identify mail servers (e.g., Google Workspace).
    
	- **`NS` records:** Identify the DNS hosting provider (e.g., INWX).
	  
	- **`TXT` records:** These are particularly valuable and can reveal:
		- **Third-party service integrations** through domain verification keys (e.g., **Atlassian**, **LogMeIn**, **Google**).
		- **Email service providers** and security configurations via SPF records (e.g., **Mailgun**, **Outlook**).
		- Internal IP addresses that may be included in SPF records.
    
- Potentially sensitive information like user IDs or account names for hosting platforms.
	  
	- ![[Pasted image 20250903114459.png]]


## References:
https://academy.hackthebox.com/module/112/section/1061
