
2025-08-18 11:50

Tags: #nmap  

## Host and Port Scanning

- To gain a **detailed understanding** of a target system after confirming it is online.

- The primary **goals** are to identify:
	- Open **ports** and their corresponding services.
	  
	- Specific **versions** of those services.
	  
	- The **operating system** of the target.
	  
	- Any **other information** provided by the services.

## Nmap Port States

- **open**: A connection was successfully established (TCP, UDP, or SCTP).

- **closed**: The port is accessible but not listening. For TCP, this is indicated by a returned packet with an `RST` (reset) flag.

- **filtered**: Nmap cannot determine if the port is open or closed, typically because a firewall is dropping packets or sending error codes.

- **unfiltered**: Occurs only in TCP ACK scans; the port is accessible, but its state (open/closed) is undetermined.

- **open|filtered**: Nmap received no response, indicating a firewall or packet filter might be present. This is common in UDP scans.

- **closed|filtered**: Used only in IP ID idle scans when it's impossible to determine if the port is closed or filtered.


## TCP Port Scanning

- **Default Scan**: Nmap's default is the **SYN scan (`-sS`)** for users with *root privileges*, which is a stealthier "half-open" scan. For *non-root users*, the default is the **TCP Connect scan (`-sT`)**.

- **Targeting Ports**: You can specify ports in various ways:
	- Individually: `-p 22,80,443`
	
	- Range: `-p 1-1024`
	
	- All ports: `-p-`
    
	- Top ports: `--top-ports=10`
    
	- Fast scan (top 100 ports): `-F`


- **TCP Connect Scan (`-sT`)**:
	- Completes the full three-way TCP handshake (`SYN`, `SYN-ACK`, `ACK`).
	  
	- **Pros**: Highly accurate and less likely to cause service instability.
	  
	- **Cons**: Not stealthy, easily logged by security systems, and slower than a SYN scan.


- **Filtered Ports Handling**:
    - **Dropped Packets**: If a firewall drops a packet, Nmap receives no response and re-transmits the packet up to a default of 10 times. This significantly slows down the scan.
      
    - **Rejected Packets**: If a firewall rejects a packet, it often sends back an ICMP message (e.g., "Port unreachable"), which Nmap uses to mark the port as `filtered`.


## UDP Port Scanning

- **Characteristics**: UDP is a stateless protocol, meaning there is no handshake to confirm delivery.
  
- **Syntax** : `-sU`
  
- **Challenges**:
    - UDP scans are significantly **slower** than TCP scans due to long timeouts.
      
    - Nmap often receives no response, making it difficult to distinguish between an `open` port and a `filtered` one.

- **State Determination**:
	- **`open`**: The target service sends a **UDP response.**
		- ![[Pasted image 20250818152232.png]]
		  
	- **`closed`**: The target sends an **ICMP "port unreachable"** message.
		- ![[Pasted image 20250818152244.png]]
		  
	- **`open|filtered`**: **No response** is received from the target.
		- ![[Pasted image 20250818152332.png]]

## Service and Version Detection (`-sV`)

- This option instructs Nmap to probe open ports to gather additional information.
  
- It can identify the exact **service name** (e.g., Samba smbd), the **version number** (e.g., 3.X - 4.X), and other configuration details.
## References:

https://academy.hackthebox.com/module/19/section/102