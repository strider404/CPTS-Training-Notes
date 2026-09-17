
2025-09-18 13:57

Tags: #web  

## Certificate Transparency Logs

- **Definition:** Certificate Transparency (CT) logs are **public, append-only records** of all issued SSL/TLS certificates. When a Certificate Authority (CA) issues a certificate, it must be submitted to these logs.
	- An **SSL/TLS certificate** is a **digital file** that authenticates a website's identity and enables an encrypted connection.


- **Purpose:**
	- **Early Detection:** They help website owners and security researchers quickly identify unauthorized or fraudulent (**rogue**) certificates.
	  
	- **Accountability:** They hold CAs accountable for their issuance practices, as any incorrect issuance is publicly visible.
	  
	- **Strengthening Security:** They improve the overall security and integrity of the web's Public Key Infrastructure (PKI).

- CT logs provide a **definitive and historical record of a domain's subdomains**, which is more reliable than guessing with wordlists or brute-forcing.
  
- They can **reveal subdomains** linked to old or expired certificates, which may host outdated and vulnerable software.

## Searching CT Logs

- **Tools:** Two popular options are **crt.sh** (a user-friendly web interface) and **Censys** (a more powerful search engine for in-depth analysis).

- **Automation:** It's possible to query the `crt.sh` API from the command line using tools like `curl` and `jq` to automate searches and filter results.
- ![[Pasted image 20250918140644.png]]

## References:

https://academy.hackthebox.com/module/144/section/1258