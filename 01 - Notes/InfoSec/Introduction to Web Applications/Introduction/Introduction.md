
2025-07-21 10:01

Tags: #web  

## Introduction

- **Web applications** are *interactive programs* that run on web browsers, utilizing a *client-server architecture.*

- They consist of a **front end** (client-side interface) and a **back end** (server-side source code and databases).


## Web Applications vs. Websites

- Traditional websites (**Web 1.0**) are **static**, meaning their content *does not change* with user interaction and must be manually updated by developers.

- Modern websites often run web applications (**Web 2.0**), featuring **dynamic content** that changes based on user input.

- Unlike static sites, web applications are *functional, modular, and designed to run on any display size or platform.*

![[Pasted image 20250721101005.png]]



## Web Applications vs. Native Operating System Applications

- **Advantages of Web Applications:**
	- **Platform-independent**: They run in a browser on any operating system without installation.
	  
	- **No local storage consumed**: The application executes on a remote server.
	  
	- **Version unity**: All users access the same, single version, simplifying updates and reducing maintenance costs.


- **Advantages of Native OS Applications:**
	- **Speed**: Faster operation as they are built to utilize native OS libraries.
	  
	- **Capability**: Deeper integration with the operating system and local hardware, not limited by browser capabilities.

- **Hybrid/Progressive Web Applications**: A modern approach *combining web technologies with native OS capabilities* for improved performance.


## Web Application Distribution

- **Open-source**: Applications like WordPress, OpenCart, and Joomla, which can be *freely used and customized.*

- **Proprietary (Closed-source)**: Applications like Wix, Shopify, and DotNetNuke, which are typically *sold* or offered via subscription.

## Security Risks and Penetration Testing

- Web applications present a **significant security challenge** due to their accessibility and large attack surface. Automated attack tools are common.

- A standard testing methodology is the **OWASP Web Security Testing Guide**, which involves reviewing both front-end and back-end components from unauthenticated and authenticated perspectives.

## Attacking Web Applications

- Web applications are a *primary target* because direct server exploitation is less common today. A minor code change can introduce a critical vulnerability.

- Examples of Common Vulnerabilities and Attacks:
	- **SQL Injection (SQLi)**: Arises from unsafe handling of user input, potentially leading to data theft, file system access, or RCE. It can be used to extract user data for password spraying attacks.
	  
	- **File Inclusion**: Can be used to read sensitive source code or achieve RCE.
	  
	- **Unrestricted File Upload**: Allows malicious code (e.g., a web shell) to be uploaded instead of an expected file type (e.g., an image), leading to server compromise.
	  
	- **Insecure Direct Object Referencing (IDOR)**: Allows a user to access or modify another user's data by manipulating object identifiers (e.g., changing a user ID in a URL).
	  
	- **Broken Access Control**: Occurs when an application fails to enforce restrictions properly, allowing privilege escalation (e.g., manipulating a `roleid` parameter during registration to become an administrator).
## References:

https://academy.hackthebox.com/module/75/section/719
