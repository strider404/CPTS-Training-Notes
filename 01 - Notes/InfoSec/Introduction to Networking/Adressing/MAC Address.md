
2025-05-06 14:47

Tags: #network  

## MAC Address

- **Media Access Control (MAC) address**:  the `physical address` for our network interfaces
	- 48 bits (6 octets)
	- Written in hexa
	- e.g., `DE:AD:BE:EF:13:37`

- *Standards* for the MAC address:
	- Ethernet (IEEE 802.3)
	- Bluetooth (IEEE 802.15)
	- WLAN (IEEE 802.11)

- *Components*:
	- **First 3 bytes (24 bits)**: *Organizationally Unique Identifier (OUI)* – assigned by IEEE to manufacturers.
	- **Last 3 bytes (24 bits)**: *Network Interface Controller (NIC)* part – **uniquely** assigned by the manufacturer.

- MAC is used in *Layer 2*. If the target is in the same subnet, the packets are delivered **directly** to the MAC. Otherwise, it is addressed to the **responsible router (default gateway)'s MAC**

- **Address Resolution Protocol (ARP)** is used in IPv4 to *determine* the MAC addresses associated with the IP addresses.

- **Locally administered / Globally unique (OUI enforced)**: the *second-least-significant bit of the first octet* is (1/0)
	- e.g., 02:00:00:00:00:00 
	- Globally unique is the MAC address assigned by the manufacturers and unique to the world
	- Locally administered is when you change your MAC address, it might not be unique to the world

- **MAC Broadcast**: data packets are transmitted simultaneously from one point to *all* members of a network
	- assigned as all 1: `FF:FF:FF:FF:FF:FF`

- **MAC Unicast / MAC Multicast**: 
	- **Unicast**: the packet sent will reach only *one* specific host
		- the last bit of the first octet is **0**
	- **Multicast**: sent only once to *all* hosts on the local network, which then decides whether or not to accept the packet based on their configuration
		- the last bit of the first octet is **1**


## Address Resolution Protocol

- **ARP (Address Resolution Protocol)**: a *Layer 2* protocol used to *map* an **IP address** (Layer 3) to a **MAC address** (Layer 2) within a **Local Area Network (LAN)**.

- **How ARP works**:
	- *ARP Request:* 
		- A device broadcasts a message:  `"Who has IP X.X.X.X? Tell me your MAC."`
	- *ARP Reply*:
		- The device with that IP replies:  `"IP X.X.X.X is at [MAC Address]"`
	- The sender stores this IP-MAC mapping in its *ARP cache*

- Example: 
	- 10.129.12.100 -> 10.129.12.255 ARP 60  Who has 10.129.12.101?  Tell 10.129.12.100
	- 10.129.12.101 -> 10.129.12.100 ARP 60  10.129.12.101 is at AA:AA:AA:AA:AA:AA

- **ARP Spoofing**:
	- Attackers send **fake ARP replies** to trick devices into linking an IP address to the **attacker’s MAC**.
	- This enables **Man-in-the-Middle (MITM)** attacks, **traffic interception**, or **data theft**.
	- Use **firewalls**, **Intrusion Detection Systems (IDS)**.

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/307)
