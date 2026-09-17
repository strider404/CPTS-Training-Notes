
2026-06-03 16:11

Tags: 

## External Information Gathering

- The engagement kicks off with a broad look at the target's external attack surface (`10.129.203.101`) to identify listening services.

- **Top 1,000 Port Scan:** A quick `nmap` scan reveals 11 open TCP ports, indicating a server running a mix of web services, email, FTP, SSH, and DNS.
    
- **Aggressive Full Port Scan:** A comprehensive scan (`nmap -p- -A`) uncovers critical details about the target (an Ubuntu host) and its services:
    - **FTP (21):** `vsftpd 3.0.3` is running and, notably, allows **Anonymous login** (a `flag.txt` file is visible).
        
    - **Web (80, 8080):** Apache HTTP servers, with port 8080 acting as a potential open proxy.
        
    - **Email (25, 110, 143, 993, 995):** Postfix (SMTP) and Dovecot (POP3/IMAP) are active.
        
    - **DNS (53):** A Bind DNS server is running, which immediately opens an avenue for subdomain enumeration.
    - ![[Pasted image 20260603161222.png]]


## Subdomain & Vhost Discovery

- With DNS active on the primary domain (`inlanefreight.local`), the next logical step is to expand the scope by uncovering additional assets.

- **DNS Zone Transfer:** Using `dig axfr`, a zone transfer is successfully executed against the target's DNS server. This misconfiguration leaks the entire DNS zone file, revealing 9 subdomains (e.g., `blog`, `dev`, `gitlab`, `vpn`).
	- ![[Pasted image 20260603164214.png]]
	    
- **Virtual Host (Vhost) Fuzzing:** To ensure no hidden assets were missed by the zone transfer, `ffuf` is used to brute-force virtual hosts.
    - _Methodology:_ First, a deliberately invalid vhost (e.g., `defnotvalid`) is requested to find the baseline "not found" response size (**15157 bytes**).
        
    - _Execution:_ `ffuf` runs through a wordlist, filtering out any responses matching that 15157-byte baseline (`-fs 15157`).
        
    - _Result:_ The fuzzer successfully identifies all the subdomains from the zone transfer, plus **one additional hidden vhost** that was not listed in DNS.
    - ![[Pasted image 20260603164259.png]]


## Environment Preparation

- To prepare for the next phase of the assessment, all discovered subdomains and vhosts are appended to the local attacker machine's `/etc/hosts` file. This allows the testing tools and browsers to resolve the internal domain names to the target's IP address (`10.129.203.101`) properly.

- **Next Steps:** With the external attack surface mapped, the focus will shift to investigating these discovered services and web applications for direct exploits or misconfigurations.
## References:

