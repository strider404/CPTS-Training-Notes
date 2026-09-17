
2025-09-06 10:06

Tags: #footprint  

## DNS

- The **Domain Name System (DNS)** is a core internet service that translates human-readable domain names (e.g., `www.google.com`) into machine-readable IP addresses (e.g., `142.250.199.68`).

- It operates as a **decentralized and globally distributed system**, much like a collection of phone books *spread across thousands of servers,* rather than a single central database.


#### DNS Server

![[Pasted image 20250906100722.png]]


- **DNS Root Server:** The highest authority, responsible for *top-level domains* (TLDs like `.com`, `.org`). There are **13** logical root servers globally.

- **Authoritative Name Server:** Holds the definitive and binding records for a specific domain (zone).

- **Non-authoritative Name Server:** This server *does not own* the original records. It answers queries by looking up information from authoritative servers and then *caching* (temporarily storing) that information.

- **Caching Server:** Temporarily *stores* (caches) DNS query results to speed up future requests for the same domain.

- **Forwarding Server:** Simply *forwards* DNS queries to another designated DNS server.

- **Resolver:** A client-side component (e.g., in your computer or router) that *initiates the DNS query process.*


#### Common DNS Records

- **A:** Maps a domain name to an IPv4 address.
  
- **AAAA:** Maps a domain name to an IPv6 address.

- **MX (Mail Exchanger):** Specifies the mail servers responsible for a domain.

- **NS (Name Server):** Indicates the authoritative name servers for a domain.

- **TXT (Text):** Provides arbitrary text information, often used for security validations like SPF or DMARC.

- **CNAME (Canonical Name):** An alias that points one domain name to another.

- **PTR (Pointer):** The reverse of an A record; maps an IP address to a domain name (reverse lookup).

- **SOA (Start of Authority):** Contains administrative information about the zone, such as the primary name server and administrator's email.


## Default Configuration

- The configuration of a **DNS server** like *BIND9* is managed through three main types of text files.
#### Local DNS Configuration Files

- These files act as the **main control panel** for the DNS server. The primary file is often `named.conf`, which is typically broken into smaller, more manageable files like `named.conf.local` and `named.conf.options`.

- **Purpose:** To define global settings and declare the "zones" (domains) that the server is responsible for.

- **Structure:**
	- **Global Options:** General settings that apply to the entire server, such as security policies or logging configurations.
	  
	- **Zone Entries:** Specific blocks of configuration that define a single domain. A zone-specific setting will always override a global one.

- Example (`named.conf.local`):
	- ![[Pasted image 20250906104306.png]]

- `zone "domain.com"`: Declares that the server is responsible for the domain `domain.com`.
  
- `type master;`: Specifies that this server is the **authoritative** (primary) source for this domain's information.
  
- `file "/etc/bind/db.domain.com";`: This is the most critical part. It tells the server to load all the **actual DNS records** for `domain.com` from the specified **zone file**.


#### Zone Files (Forward Lookup)

- This file is the "phone book" for a domain. It contains all the records needed for **forward lookup**, which is the process of translating a domain name (like `www.domain.com`) into an IP address.

- **Purpose:** To store all the resource records (A, CNAME, MX, etc.) associated with a single domain.
  
- **Format:** It uses the industry-standard **BIND file format**. A syntax error in this file can make the entire domain unresponsive.

![[Pasted image 20250906104707.png]]


- **Key Components:**
	- **SOA (Start of Authority) Record:** A mandatory record at the beginning of the file that contains administrative details like the primary name server, an administrator's contact info, and timers for how other servers should cache its data.
	
	- **NS (Name Server) Records:** At least one NS record is required to declare the authoritative name servers for the domain.
    
	- **Other Records:** The file then lists other records like:
	    - **A records** to map hostnames to IPv4 addresses (e.g., `server1 IN A 10.129.14.5`).
        
	    - **CNAME records** to create aliases (e.g., `ftp IN CNAME server1`).
        
	    - **MX records** to define mail servers.

#### Reverse Name Resolution Zone Files (Reverse Lookup)

- This file does the opposite of a standard zone file. It is used for **reverse lookup**, which translates an IP address back into its associated hostname (e.g., `10.129.14.5` resolves to `server1.domain.com`).

- **Purpose:** To map IP addresses back to their **Fully Qualified Domain Names (FQDNs).**
  
- **Key Record:** The primary record type used here is the **PTR (Pointer)** record.

![[Pasted image 20250906104945.png]]


## Footprinting

- **Dangerous Settings:** Misconfigurations can expose the server to attack. Key settings to secure are:
    - `allow-query`: Restricts who can make queries.
      
    - `allow-recursion`: Restricts who can make recursive queries.
      
    - `allow-transfer`: Restricts who can request a full copy of a zone file.

#### Enumeration Techniques

- **NS/ANY Queries:** Using tools like `dig` to ask a server for all its known records (`ANY`) or its designated name servers (`NS`).
	- ![[Pasted image 20250906105705.png]]
	- ![[Pasted image 20250906105724.png]]


- **Version Query:** Sometimes, a server's version can be queried, revealing potential vulnerabilities.
	- ![[Pasted image 20250906105740.png]]


- **Zone Transfer (AXFR):** A *critical vulnerability* occurs when `allow-transfer` is misconfigured. An attacker can request a full copy of the zone file, revealing all hostnames, subdomains, and potentially internal network IP addresses.
	- ![[Pasted image 20250906105818.png]]


- **Subdomain Brute-Forcing:** Using *wordlists* and *tools* like `dnsenum` to systematically guess and identify valid subdomains of a target domain.
	- Example: `dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb`
## References:

https://academy.hackthebox.com/module/112/section/1069