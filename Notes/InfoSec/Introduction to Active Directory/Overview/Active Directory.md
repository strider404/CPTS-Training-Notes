
2025-07-04 09:33

Tags: #ad  

## What is Active Directory

- A **centralized directory (database) service** for Windows network environments.

- Manages resources like *users, computers, groups, and policies* in a hierarchical structure.
	- like a database, it contains all usernames, passwords, etc in 1 place so employees don't have to create their own accounts in each separated computers 

- Provides **authentication and authorization** for a Windows domain.

- **Active Directory Domain Services (AD DS)** (a service within AD) stores and manages access to directory data, such as user credentials.

- Highly **scalable**, supporting millions of objects.

- Widely used

![[Pasted image 20250704094119.png]]


#### High-value target

- **Insecure by Design**: It is designed for backward compatibility, not always with security as the default. It's prone to misconfigurations.

- **Open by Nature**: It acts as a large, read-only database accessible to all domain users. Even a basic user account can enumerate the domain to find flaws.

- **High-Value Target**: Its widespread use makes it a primary focus for attackers, including ransomware operators like Conti.

- **Critical Vulnerabilities**: Flaws such as PrintNightmare (CVE-2021-34527) and Zerologon (CVE-2020-1472) have been exploited to gain complete control over networks.

## References:

[Introduction to Active Directory](https://academy.hackthebox.com/module/74/section/699)