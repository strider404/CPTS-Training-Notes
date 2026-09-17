
2025-09-18 10:09

Tags: #web  

## Subdomains

- **Subdomains** are **extensions of a primary domain** used to organize different sections of a website (e.g., `blog.example.com`, `shop.example.com`).

- **Why Subdomains Matter for Reconnaissance:**
	- They can host less secure **development and staging environments**.
	  
	- They might contain **hidden login portals** for administrative access.
	  
	- They could run vulnerable **legacy applications**.
	  
	- They may inadvertently expose **sensitive information** and configuration files.


## Subdomain Enumeration

- This is the process of systematically discovering a domain's subdomains.
  
- Subdomains are typically represented by `A`, `AAAA`, or `CNAME` DNS records.


- **Active Enumeration:** Involves directly interacting with the target's DNS servers.
	- **DNS Zone Transfer:** An attempt to get a full list of DNS records from a misconfigured server; rarely successful.
	  
	- **Brute-force:** Systematically trying a wordlist of common names against the domain using tools like `dnsenum`, `ffuf`, and `gobuster`.


- **Passive Enumeration:** Uses external, public sources without directly contacting the target's servers.
	- **Certificate Transparency (CT) Logs:** Publicly available SSL/TLS certificates often list associated subdomains.
	  
	- **Search Engines:** Using operators like `site:example.com` to find indexed subdomains.
	  
	- **Online DNS Databases:** Websites that aggregate public DNS data.

- **Combining** both **active** (more comprehensive but detectable) and **passive** (stealthier but potentially incomplete) methods provides the most effective results.



## References:

https://academy.hackthebox.com/module/144/section/1252