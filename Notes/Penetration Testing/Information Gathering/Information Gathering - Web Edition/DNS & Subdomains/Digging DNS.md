
2025-09-17 10:58

Tags: #web  

## Digging DNS

- **DNS Reconnaissance:** This is the practice of using tools to query DNS servers to gather information for web reconnaissance. It is crucial to be cautious and respect rate limits to avoid being blocked.

## DNS Tools

- **`dig` (Domain Information Groper):** A versatile and powerful tool for **detailed DNS queries.**
  
  
- **`nslookup` & `host`:** Simpler tools for basic and quick DNS lookups.
  
  
- **`dnsenum`, `fierce`, `dnsrecon`:** Automated tools for comprehensive enumeration, such as discovering subdomains.
  
  
- **`theHarvester`:** An OSINT tool that gathers information, including DNS records, from multiple public sources.
  
  
- **Online DNS Lookup Services:** Web-based interfaces that provide a user-friendly way to perform DNS lookups.

## The `dig` Command

![[Pasted image 20250917110351.png]]



## Groping DNS

![[Pasted image 20250917110443.png]]

- **Header**
    - `;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449`: This line indicates the **type of query** (`QUERY`), the **successful status** (`NOERROR`), and a u**nique identifier** (`16449`) for this specific query.
        - `;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0`: This describes the **flags** in the DNS header:
            - `qr`: Query Response flag - indicates this is a response.
            - `rd`: Recursion Desired flag - means recursion was requested.
            - `ad`: Authentic Data flag - means the resolver considers the data authentic.
            - The remaining numbers indicate the number of entries in each section of the DNS response: 1 question, 1 answer, 0 authority records, and 0 additional records.


- **Question Section**
    - `;google.com. IN A`: This line specifies the **question**: "What is the IPv4 address (A record) for `google.com`?"


- **Answer Section**
    - `google.com. 0 IN A 142.251.47.142`: This is the **answer** to the query. It indicates that the IP address associated with `google.com` is `142.251.47.142`. The '`0`' represents the `TTL` (time-to-live), indicating how long the result can be cached before being refreshed.


- **Footer**
    - `;; Query time: 0 msec`: This shows the time it took for the query to be processed and the response to be received (0 milliseconds).
      
    - `;; SERVER: 172.23.176.1#53(172.23.176.1) (UDP)`: This identifies the DNS server that provided the answer and the protocol used (UDP).
      
    - `;; WHEN: Thu Jun 13 10:45:58 SAST 2024`: This is the timestamp of when the query was made.
      
    - `;; MSG SIZE rcvd: 54`: This indicates the size of the DNS message received (54 bytes).

## References:

https://academy.hackthebox.com/module/144/section/1251