
2025-09-17 10:35

Tags: #web  

## DNS

- **Function:** DNS, or the Domain Name System, acts as a translator for the internet. It converts human-readable domain names (e.g., `www.example.com`) into numerical IP addresses (e.g., `192.0.2.1`) that computers use to identify each other on a network.


## How DNS Works

![[Pasted image 20250917104830.png]]

- **DNS Query:** When you enter a domain name, your computer first checks its **local cache**. If the IP address isn't found, it asks a DNS Resolver (typically from your ISP).
  
- **Recursive Lookup:** The resolver checks **its own cache**. If the entry is not present, it initiates a lookup process starting with a Root Name Server.
  
- **Root Server:** The Root Server directs the resolver to the appropriate **Top-Level Domain (TLD) Name Server** (e.g., the one for **`.com` domains**).

- **TLD Server:** The TLD Name Server points the resolver to the specific **Authoritative Name Server** responsible for the requested domain (e.g., **`example.com`**).
  
- **Authoritative Server:** This server holds the **definitive IP address** for the domain and sends it back to the resolver.
  
- **Response:** The resolver returns the IP address to your computer and caches it for future use. Your computer can now connect directly to the website's server.


#### The `hosts` File

- **Purpose:** A local text file on an operating system that manually **maps hostnames to IP addresses.**

- **Function:** Entries in the `hosts` file **override** the standard DNS resolution process.
  
- **Use Cases:** Commonly used for web development (redirecting a domain to a local server), network troubleshooting, and blocking access to specific websites.
  
- **Location:**
    - **Windows:** `C:\Windows\System32\drivers\etc\hosts`
      
    - **Linux/macOS:** `/etc/hosts`

![[Pasted image 20250917105142.png]]



## DNS Concepts

- **Zone:** A managed portion of the domain namespace (e.g., **`example.com` and all its subdomains)**.

- **Zone File:** A text file on a DNS server that contains **all the resource records** for a specific zone.

- **DNS Records:** Entries within a zone file that provide information about the domain. Common types include:
	- **A:** Maps a hostname to an IPv4 address.
	  
	- **AAAA:** Maps a hostname to an IPv6 address.
	  
	- **CNAME (Canonical Name):** Creates an alias from one hostname to another.
	  
	- **MX (Mail Exchange):** Specifies the mail servers for a domain.
	  
	- **NS (Name Server):** Identifies the authoritative name servers for a zone.
	  
	- **TXT (Text):** Stores arbitrary text, often for verification or security policies like SPF.
	  
	- **SOA (Start of Authority):** Contains administrative information about the zone.
	  
	- **PTR (Pointer):** Maps an IP address back to a hostname for reverse DNS lookups.


- **Key concepts:**

|DNS Concept|Description|Example|
|---|---|---|
|`Domain Name`|A human-readable label for a website or other internet resource.|`www.example.com`|
|`IP Address`|A unique numerical identifier assigned to each device connected to the internet.|`192.0.2.1`|
|`DNS Resolver`|A server that translates domain names into IP addresses.|Your ISP's DNS server or public resolvers like Google DNS (`8.8.8.8`)|
|`Root Name Server`|The top-level servers in the DNS hierarchy.|There are 13 root servers worldwide, named A-M: `a.root-servers.net`|
|`TLD Name Server`|Servers responsible for specific top-level domains (e.g., .com, .org).|[Verisign](https://en.wikipedia.org/wiki/Verisign) for `.com`, [PIR](https://en.wikipedia.org/wiki/Public_Interest_Registry) for `.org`|
|`Authoritative Name Server`|The server that holds the actual IP address for a domain.|Often managed by hosting providers or domain registrars.|
|`DNS Record Types`|Different types of information stored in DNS.|A, AAAA, CNAME, MX, NS, TXT, etc.


## References:

https://academy.hackthebox.com/module/144/section/3074