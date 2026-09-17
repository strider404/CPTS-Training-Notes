
2025-09-17 08:39

Tags: #web  

## Introduction

- Web reconnaissance is the initial phase of information gathering in a security assessment or penetration test. It involves methodically collecting data about a target website or web application. This process is crucial for:
	- **Identifying assets:** Discovering all public components like subdomains, IP addresses, and technologies used.
	  
	- **Finding hidden information:** Locating sensitive files, such as backups or configurations.
	  
	- **Analyzing the attack surface:** Assessing the target's weaknesses and potential entry points.
	  
	- **Gathering intelligence:** Collecting information for further exploitation or social engineering.

## Types of Reconnaissance

- Web reconnaissance is divided into two primary types: **active** and **passive**.

- **Active Reconnaissance:** This method involves **direct interaction** with the target system. While it provides a more comprehensive view, it carries a **higher risk of being detected by security systems**. Common techniques include:
	- **Port Scanning:** Identifying open ports and services.
    
	- **Vulnerability Scanning:** Probing for known weaknesses.
    
	- **Network Mapping:** Discovering the network topology.
    
	- **Banner Grabbing:** Retrieving service information from banners.
    
	- **OS Fingerprinting:** Identifying the operating system.
    
	- **Service Enumeration:** Determining specific service versions.
    
	- **Web Spidering:** Crawling the website to map its structure.



- **Passive Reconnaissance:** This method involves gathering information **without direct interaction** with the target. It relies on **publicly available information** and is much stealthier, with a very low risk of detection. However, it may provide less comprehensive data. Common techniques include:
	- **Search Engine Queries:** Using search engines to find public information.
    
	- **WHOIS Lookups:** Retrieving domain registration details.
    
	- **DNS Analysis:** Examining DNS records to identify infrastructure.
    
	- **Web Archive Analysis:** Viewing historical versions of a website.
    
	- **Social Media Analysis:** Gathering information from public social media profiles.
    
	- **Code Repositories:** Searching for exposed credentials or vulnerabilities in public code.
## References:

https://academy.hackthebox.com/module/144/section/1247