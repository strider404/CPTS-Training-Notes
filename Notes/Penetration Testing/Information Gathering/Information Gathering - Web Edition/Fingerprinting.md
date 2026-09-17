
2025-09-18 14:12

Tags: #web  

## Fingerprinting

- **Definition**: Fingerprinting is the technique of **extracting detailed technical information about the technologies that power a website**. This includes identifying the web server, operating system, frameworks, and other software components.


- **Techniques**:
    - **Banner Grabbing**: Analyzing banners from web servers which often reveal software names and versions.
      
    - **HTTP Header Analysis**: Inspecting headers like `Server` and `X-Powered-By` for technology information.
      
    - **Probing**: Sending specially crafted requests to elicit unique responses characteristic of specific software.
      
    - **Content Analysis**: Examining a page's structure, scripts, and copyright notices for clues about the underlying technology.


- **Common Tools**:
	- **Technology Profilers**: Wappalyzer, BuiltWith, WhatWeb.
	  
	- **Network Scanners**: Nmap.
	  
	- **WAF Detectors**: `wafw00f` **(Web Application Firewall detector)**.
	  
	- **Web Server Scanners**: Nikto.


#### Reconaissance

- `whatweb` can also be used
	- ![[Pasted image 20250918150900.png]]


- **Banner Grabbing (`curl`)**: Identified the server as `Apache/2.4.41 (Ubuntu)` and revealed the use of `WordPress` through the `X-Redirect-By` header.
	- Can specify the **vhost** by adding the **Host** header
		- `-H "Host: xxx.xxx.com"`
	- ![[Pasted image 20250918141835.png]]
	- Redirect to `https://inlanefreight.com` => get that banner
	- ![[Pasted image 20250918141917.png]]
	- Continue with `https://www.inlanefreight.com`
	- ![[Pasted image 20250918141940.png]]


- **WAF (Web Application Firewall) Detection (`wafw00f`)**: Determined that the site is protected by the `Wordfence` WAF.
	- ![[Pasted image 20250918142019.png]]


- **Web Server Scanners (`Nikto`)**:
	- ![[Pasted image 20250918142157.png]]
	- Confirmed the server is an outdated version of Apache.
    
	- Found a WordPress installation, including the login page (`/wp-login.php`).
    
	- Reported several potential security issues, such as missing security headers (e.g., `Strict-Transport-Security`) and the presence of a `license.txt` file that could disclose information.

## References:

