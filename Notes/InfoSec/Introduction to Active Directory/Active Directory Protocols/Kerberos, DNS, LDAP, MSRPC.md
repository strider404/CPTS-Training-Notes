
2025-07-10 10:57

Tags: #ad 

## 4 main Protocols in AD

#### Kerberos

- **Function:** Handles *authentication* for domain accounts in Windows environments since Windows 2000.

- **Process:** It is a *stateless* (do not store anything) protocol that uses a *ticket-based system* instead of sending passwords over the network.
	- **Steps**:

![[Pasted image 20250710110822.png]]


- **Security:** This method prevents user credentials from being transmitted directly over the network.
	- Because it is sent to the **KDC (Key Distribution Center)**

- **Port:** Uses port **88 (TCP/UDP)**.


#### DNS (Domain Name System)

- **Function:** Enables clients to *locate Domain Controllers* and other services by resolving hostnames to IP addresses.

- **Mechanism:** Active Directory uses **Service (SRV) records** in DNS to publish and *locate available services.*

- **Dynamic DNS:** Automatically updates DNS records when a system's IP address changes, reducing manual administration.

- **Lookup Types:**
	- **Forward Lookup:** Converts a hostname to an IP address.
	  
	- **Reverse Lookup:** Converts an IP address to a hostname.

- **Port:** Uses port **53 (primarily UDP, with TCP as a fallback)**.

![[Pasted image 20250710113058.png]]


#### LDAP (Lightweight Directory Access Protocol)

- **Function:** An application protocol for *directory lookups*. It's the "language" that applications use to talk to Active Directory.

- **Analogy:** The relationship between Active Directory and LDAP is similar to that of an Apache web server and the HTTP protocol.

- **Authentication**:
	- **Simple Authentication:** Uses a username and password.
	- **SASL (Simple Authentication and Security Layer):** Binds to the LDAP server using other authentication frameworks, like Kerberos.

- **Security Concern:** By default, LDAP authentication messages are sent in *cleartext*. Using LDAP over SSL (LDAPS) is recommended.

- **Ports:**
	- **LDAP:** Port **389**
	  
	- **LDAPS:** Port **636**

![[Pasted image 20250710151535.png]]


#### MSRPC (Microsoft Remote Procedure Call)

- **Function:** Microsoft's implementation of **RPC**, which *facilitates* *communication* between client-server applications.

- Windows systems use **MSRPC** to access systems in Active Directory using four key RPC interfaces:
	- **lsarpc:** Manages local security policies on a machine.
    
    - **netlogon:** Authenticates users and services within the domain.
    
    - **samr:** Manages the domain account database (users and groups). Attackers can use this for reconnaissance.
    
    - **drsuapi:** Manages directory replication between Domain Controllers. Attackers can abuse this to replicate the Active Directory database (`NTDS.dit`) and extract password hashes.


## References:

https://academy.hackthebox.com/module/74/section/701