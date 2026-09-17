
2025-06-16 12:54

Tags: #network  

## Domain Name System (DNS)

- DNS: acts as the internet's directory, *translating* human-readable **domain names** (e.g., `www.google.com`) into machine-readable **IP addresses** (e.g., `93.184.216.34`)


#### DNS Hierarchy

| **Layer**                  | **Description**                                                                   |
| -------------------------- | --------------------------------------------------------------------------------- |
| *Root Servers*             | The top of the DNS hierarchy.                                                     |
| *Top-Level Domains (TLDs)* | Such as `.com`, `.org`, `.net`, or country codes like `.uk`, `.de`.               |
| *Second-Level Domains*     | For example, `example` in `example.com`.                                          |
| *Subdomains or Hostname*   | For instance, `www` in `www.example.com`, or `accounts` in `accounts.google.com`. |

![[Pasted image 20250616125850.png]]


#### DNS Resolution Process (Domain Translation)

- Your computer first checks its **local DNS cache**.

- If the address is not found, it queries a **recursive DNS server** (often from your ISP).

- The recursive server contacts a **root server**.

- The root server directs it to the correct **TLD name server** (e.g., for `.com`).

- The TLD server points to the domain's **authoritative name server**.

- The authoritative server provides the final IP address.

- This IP address is sent back to your computer, allowing it to connect to the website's server.

![[Pasted image 20250616130239.png]]
## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3241)