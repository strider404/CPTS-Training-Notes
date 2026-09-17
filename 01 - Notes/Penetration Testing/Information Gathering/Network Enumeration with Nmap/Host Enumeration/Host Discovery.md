
2025-08-18 10:34

Tags: #nmap  

## Host Discovery

- **Host Discovery** is the initial phase of a penetration test, designed to *identify which systems are online and active within a network*. The primary tool discussed for this purpose is **Nmap**.

- It is a recommended best practice to **store all scan results** (`-oA` flag) for documentation, comparison, and reporting.

#### Methods for Specifying Targets

- **Scan Network Range:** Scans an *entire* network segment.
	- **Command:** `sudo nmap <network/CIDR> -sn`
	  
	- **Example:** `sudo nmap 10.129.2.0/24 -sn`


- **Scan IP List:** Scans a list of targets provided in a *file*.
	- **Command:** `sudo nmap -sn -iL <file_name>`
	  
	- **Example:** `sudo nmap -sn -iL hosts.lst`


- **Scan Multiple IPs:** Scans *several specific* IP addresses.
	- **Command (Separate IPs):** `sudo nmap -sn <IP1> <IP2> ...`
	  
	- **Command (IP Range):** `sudo nmap -sn <network.start-end>`
	  
	- **Example:** `sudo nmap -sn 10.129.2.18-20`


- **Scan Single IP:** Scans *one specific* target to determine if it is online.
	- **Command:** `sudo nmap <target_IP> -sn`

#### ARP Request vs ICMP Echo Request

- **ARP** Request can only be used for your **local network**

- **ICMP** Echo Request work for hosts across **the Internet**

#### Nmap Options for Host Discovery

- `-sn`: **Disables port scanning**, instructing Nmap to only perform **host discovery** (also known as a "ping scan").

- `-oA <filename>`: **Stores** the scan results in all available formats (Normal, XML, and Grepable), using the specified filename as a prefix.

- `-iL <filename>:` **Reads** the list of targets from the specified file.

- `-PE:` Explicitly uses an **ICMP Echo Request** to perform the ping scan.
	- Why, because if not, it might use **ARP request** and ARP reply
	- ![[Pasted image 20250818112039.png]]

- `--packet-trace:` **Displays all packets sent and received** during the scan, which is useful for debugging.

- `--reason:` **Explains** why Nmap concluded a host is up or down.

- `--disable-arp-ping:` **Prevents Nmap from using ARP requests** for host discovery on the local network.

![[Pasted image 20250818114653.png]]
## References:

https://academy.hackthebox.com/module/19/section/101