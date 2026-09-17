
2025-09-11 16:01

Tags: #footprint  

## IPMI

- **Definition**: The Intelligent Platform Management Interface (IPMI) is a *standardized set of specifications for a hardware-based system* that allows for out-of-band management and monitoring of computer systems.

- **Functionality**: It operates **independently** of the host's operating system, BIOS, and CPU. This autonomy allows administrators to manage a server even if it is powered off, unresponsive, or has no OS installed.


- **Common Uses**:
	- Modifying BIOS settings before the OS boots.
	  
	- Powering a host on or off remotely.
	  
	- Accessing a host after a system failure.
	  
	- Monitoring hardware vitals like temperature, voltage, fan speed, and power supplies.
	  
	- Reviewing hardware logs and querying inventory.


- **Core Component**: The **Baseboard Management Controller (BMC)** is a dedicated **microcontroller**, often an embedded ARM system running Linux, that is the heart of the IPMI system.

- **Communication**: IPMI primarily uses UDP port **623**.

- **Common Vendor Implementations**:
	- Hewlett Packard (HP): Integrated Lights-Out (iLO)
	- Dell: Dell Remote Access Controller (DRAC)
	- Supermicro: Supermicro IPMI


## Security Risks and Exploitation

- Gaining access to a BMC is considered almost equivalent to **having physical access** to the server. The primary attack vectors are:

- **Default Credentials**:
	- Administrators frequently **fail to change the default passwords** on BMCs.
	- Examples include `ADMIN:ADMIN` for Supermicro IPMI and `root:calvin` for Dell iDRAC.
	- These credentials can provide access to web consoles or command-line interfaces like SSH/Telnet.

## Footprinting

- **Nmap**
	- ![[Pasted image 20250911161104.png]]



- **IPMI 2.0 RAKP Protocol Flaw**:
	- **Vulnerability**: During the authentication handshake, the server **sends a salted SHA1 or MD5 hash** of a user's password to the client _before_ the client has successfully authenticated.
	  
	- **Exploitation**: An attacker can *request this hash for any valid username without needing the password*. The captured hash can then be taken offline and cracked using dictionary or brute-force attacks with tools like **Hashcat (mode 7300).**
		- Just use `-a 0` (**dictionary attack**) and the Seclists wordlist
		- Remember to **include the username** to the hash and use `--username` option
			- e.g., `admin:1093299fkafd....dael`, must include the **admin**, not only the password hash
			  
			  
	- **Tools**: The **Metasploit Framework** has modules (`ipmi_version`, `ipmi_dumphashes`) specifically for identifying IPMI services and capturing these hashes.
		- ![[Pasted image 20250911161011.png]]
		- ![[Pasted image 20250911161024.png]]
		  
		- A successful attack **grants an adversary complete control** over the host machine, including the ability to power it on/off, reinstall the operating system, or monitor all activity.
		  
		- The RAKP protocol flaw is inherent to the IPMI 2.0 specification and **cannot be "patched."**



## References:
