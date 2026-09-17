
2025-09-18 10:45

Tags: #web  

## DNS Zone Transfers

- **DNS zone transfer** is a mechanism used to *copy all DNS records for a specific domain* (a "zone") from a **primary DNS server to a secondary DNS server.**

- Its legitimate purpose is to ensure **consistency and redundancy** across multiple name servers.

![Diagram showing data transfer between secondary and primary servers. Includes steps: XML Request, XML Record, loop for retries, XML Report, and AOK (Acknowledgment).](https://mermaid.ink/svg/pako:eNqNkc9qwzAMxl9F-JSx7gV8KISWXcY2aHYYwxdjK39obGWKvBFK333ukg5aGNQnW9b3Q_q-g3LkUWk14mfC6HDb2YZtMBHyGdFR9JanCvkL-WG9vh-4C38FDeX74w52J-0oUHxQRHhjG8ca-W5mXAgy4YqpoXotM8EReygqsSxANZRJWuJOpoXSEw0gC3ku3QTfvlQLfBZh9DeOdbELbCgMPQr-58u1LZsnKEq3j_Tdo28wYJS8iVqpgBxs57PjhxPLKGnzr1E6XzNxb5SJx9xnk1A1Rae0cMKVYkpNq3Rt-zG_0uCtnLM6t6DvhPh5zvM31uMPG8qm-A)


1. **Request Initiation**: The secondary DNS server sends a zone transfer request to the primary server. This is typically an `AXFR` (Full Zone Transfer) query.
   
2. **SOA Record Response**: The primary server first responds by sending its **Start of Authority (`SOA`) record**. This record contains administrative details about the zone, most importantly a serial number that the secondary server uses to verify if its own copy of the zone file is outdated.
   
3. **Transmission of Records**: After sending the `SOA` record, the primary server transmits all other DNS records within the zone (e.g., `A`, `AAAA`, `MX`, `CNAME`, `NS`) to the secondary server.
   
4. **Signal of Completion**: Once all records have been sent, the primary server signals the end of the transfer.
   
5. **Acknowledgment**: The secondary server sends an acknowledgment (`ACK`) message back to the primary server, confirming that it has successfully received the complete zone data.


## Vulnerability

- A significant security vulnerability arises when a DNS server is **misconfigured** to *allow zone transfer requests from any client*, not just trusted secondary servers.

- An unauthorized zone transfer can provide a comprehensive map of a target's **DNS infrastructure**, revealing:
	- A **complete list of subdomains**, including those that may be *hidden* or used for internal purposes (e.g., development, staging, admin panels).
	  
	- The **IP addresses** associated with each subdomain.
	  
	- Details about the domain's **authoritative name servers** and other record types (`MX`, `CNAME`, etc.).

- Attackers or security professionals can attempt a zone transfer using tools like the `dig` command.
  
- The specific **command** to request a full zone transfer (`AXFR`) is: `dig axfr @<dns-server> <domain-name>`.
  
- If the server is vulnerable, it will return the entire list of DNS records for the specified domain.
## References:

https://academy.hackthebox.com/module/144/section/1255