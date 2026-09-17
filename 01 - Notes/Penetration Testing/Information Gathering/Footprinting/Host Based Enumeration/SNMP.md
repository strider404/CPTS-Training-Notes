
2025-09-10 14:56

Tags: #footprint  

## SNMP

- **Simple Network Management Protocol (SNMP):** A protocol designed for *monitoring and managing network devices* such as routers, switches, and servers. 
  
- It operates over **UDP**.

- **Ports**:
	- **Port 161**: queries and commands
	- **Port 162**: receiving unsolicited alerts called "traps"


- **Management Information Base (MIB):** A *standardized text file*, written in Abstract Syntax Notation One (ASN.1), that *defines the structure of manageable objects* on a device. It acts as a **map**, describing what information can be queried, but does not contain the data itself. It organizes objects in a hierarchical **tree** structure.


- **Object Identifier (OID):** A *unique, dot-separated numerical address* that *points to a specific object* (a piece of information, like CPU temperature or a network interface's status) within the MIB tree.


## SNMP Versions and Security

- **SNMPv1:** The original version. It **lacks authentication and encryption**. All data, including the password-like "community string," is transmitted in plaintext, making it highly insecure.

- **SNMPv2c:** An updated version that added some functions but remains insecure. The 'c' stands for "community-based," and like v1, it transmits community strings in **plaintext**, offering no significant security improvement.

- **SNMPv3:** The current and most secure version. It introduces critical security features, including **user-based authentication** (username/password) and **encryption** of data packets. However, this increased security comes with a significant increase in configuration complexity.


## Security Vulnerabilities and Risks

- **Community Strings:** These function as *passwords* for SNMPv1 and v2c. Because they are sent in *plaintext*, they can be easily **intercepted** through network sniffing. Many devices use default, well-known community strings like "**public**" (for read-only access) and "**private**" (for read-write access).


- **SNMP Daemon Config:** 
	- Locate in `/etc/snmp/snmpd.conf`


- **Dangerous Configurations:** Administrators may misconfigure SNMP, creating critical vulnerabilities. Examples include:
	- `rwuser noauth`: Grants full read-write access to the entire OID tree without any authentication.
	  
	- `rwcommunity <string>`: Grants full read-write access to any device that knows the community string.


## Footprinting

- **snmpwalk:** A command-line tool used to "walk" the MIB tree of a target device and retrieve all accessible OID values, given a valid community string.
	- ![[Pasted image 20250910150459.png]]


- **onesixtyone:** A fast *brute-force tool* designed to discover **valid community strings** by testing them against a target from a wordlist.
	- ![[Pasted image 20250910150532.png]]
	- ![[Pasted image 20250916105724.png]]
	- The community string in the above case is **backup**


- **braa:** A tool used to *query SNMP devices*. It can be used to *brute-force* and *enumerate OIDs* **once a community string is known.**
	- ![[Pasted image 20250910150611.png]]
## References:

https://academy.hackthebox.com/module/112/section/1075v