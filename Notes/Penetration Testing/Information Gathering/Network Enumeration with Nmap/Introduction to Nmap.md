
2025-08-18 09:57

Tags: #nmap  

## Introduction to Nmap

- **Network Mapper (Nmap)** is an open-source tool for *network analysis* and security auditing.

- **Core Capabilities**:
	- **Host Discovery**: Identifies available hosts on a network using raw packets.
	  
	- **Service & OS Detection**: Determines services, applications (including names and versions), and operating systems running on hosts.
	  
	- **Security Auditing**: Checks for the presence and configuration of packet filters, firewalls, and Intrusion Detection Systems (IDS).
#### Use Cases

- *Auditing network security*
  
- *Simulating penetration tests.*

- *Verifying firewall and IDS configurations.*

- *Network mapping.*

- *Identifying open ports.*

- *Vulnerability assessment.*

#### Scanning Techniques

- Host discovery.

- Port scanning.

- Service enumeration and detection.

- OS detection.

- Scriptable interaction via the **Nmap Scripting Engine (NSE)**.

## Syntax

- `nmap <scan types> <options> <target>`

- Always use **sudo** with `nmap` whenever possible, why:
	- When combining with sudo, nmap will use `-sS` by default instead of `-sT`
		- `-sS` sends only the *SYN* packages, which is stealthier and faster (can only operate with **sudo**)
		- `-sT` completes a *full three-way TCP handshake*,  which is more likely to be logged and slower
	- Allow OS detection (`-O`)

- **Port State Determination (using -sS)**:
	- **Open**: Target responds with a `SYN-ACK` packet.
	  
	- **Closed**: Target responds with an `RST` packet.
	  
	- **Filtered**: No response is received, suggesting a firewall dropped the packet.
## References:

https://academy.hackthebox.com/module/19/section/100