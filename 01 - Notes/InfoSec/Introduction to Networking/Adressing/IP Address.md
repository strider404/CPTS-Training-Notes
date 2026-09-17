
2025-05-01 16:17

Tags: #network  

## Addresses

- **MAC (Media Access Control) address**: identify devices ==within a local network==

- **IP addresses (IPv4/IPv6)**: required for communicating ==with the remote network==

- IP address used in *Layer 3*, while MAC is used in *Layer 2*

- IP is the address of the building, and MAC is the exact apartment number

## IPv4 Structure

- **32-bit** (4 bytes) structure, divided into **four 8 bits** (from 0-255), each 8 bits separated by a dot
	- e.g., Binary: 0111 1111.0000 0000.0000 0000.0000 0001 | Decimal: 127.0.0.1

- Each network interface (network cards, network printers, or routers) is assigned a **unique** IP address (about 4 billion unique addresses)

- **2 parts**: network part and the host part

- Overall structure:

| `Class` | **Starting Bits** | **Network Address** | **First Address** | **Last Address** | **Subnetmask** | **CIDR**  | **Subnets** | **IPs**        |
| ------- | ----------------- | ------------------- | ----------------- | ---------------- | -------------- | --------- | ----------- | -------------- |
| `A`     | 0                 | 1.0.0.0             | 1.0.0.1           | 127.255.255.255  | 255.0.0.0      | /8        | 127         | 16,777,214 + 2 |
| `B`     | 10                | 128.0.0.0           | 128.0.0.1         | 191.255.255.255  | 255.255.0.0    | /16       | 16,384      | 65,534 + 2     |
| `C`     | 110               | 192.0.0.0           | 192.0.0.1         | 223.255.255.255  | 255.255.255.0  | /24       | 2,097,152   | 254 + 2        |
| `D`     | 1110              | 224.0.0.0           | 224.0.0.1         | 239.255.255.255  | Multicast      | Multicast | Multicast   | Multicast      |
| `E`     | 1111              | 240.0.0.0           | 240.0.0.1         | 255.255.255.255  | reserved       | reserved  | reserved    | reserved       |
- **Class**: 
	- Defined by the ==first few bits== of the IP address
		- e.g., with Class B, starting bit is 10 (binary), then the IP range will be from ==10==00 0001.0000 0000.0000 0000.0000 0000 (the first 8 bits must not be 0) to ==10==11 1111.1111 1111.1111 1111. 1111 1111
	- Class differs in the number of hosts
		- e.g., class A can have millions of hosts while class C can only have 254

- **Subnet Mask**: 
	- 32-bit to identify which part is the ==network part== and which part is the ==host part==
	- **255** is the network part
	- **0** is the host part

- ==Notice the +2 in the IP column==, it is the network address and the broadcast address which can't be assigned to any host

- **Network address**: 
	- The ==first== address in any subnet
	- It represents the **entire subnet** and **cannot be assigned to any host**.
	- Used by routers and systems to **identify the subnet**
	- If the subnet is the **same** with the source and the destination, the packets are routed within the subnet, but if is **not**, they will be transported to default gateway
	- Use **ANDing** to do the above:
		- Compare ==each bit== of the IP with the subnet mask using AND -> get the network address (because the host part of subnet mask is always 0 -> using AND with the IP in the host part-> get 0s -> the network address)
	- The ==host part== of the IP is set to **0**

- **Broadcast Address**:
	- The ==last== address in the subnet
	- **To send packets to all hosts on the subnet simultaneously**
		- When:
			- ARP (when the device's MAC is unknown)
			- DHCP (when the device don't have the IP)
	- The host part of the IP is set to **1**

- **Default Gateway**:
	- The IP address of the **Router**, to send packets to another subnet or outside network (including the Internet)
	- Acts as an exit point
	- Can be the ==first== or the ==last== address

- **CIDR (Classless Inter-Domain Routing)**:
	- A method of **IP address allocation and routing** that **replaces** the older **classful addressing**
	- The division based on subnet mask is also called ==CIDR suffix==
	- **Indicates how many bits from the beginning are 1 (belong to the network part)**
	- e.g., `/24` means 24 bits are from the network part, 8 last bits are from the host part
		- The subnet mask is 255.255.255.0
		- CIDR: `192.168.10.39/24`

![[Pasted image 20250514105202.png]]

- **Public vs Private IPv4 address**: because there are limited IPv4 addresses
	- -> only the router need the IP address that is unique to the world (*Public address*) (provided by the ISP)
	- Other devices in the network will have *Private address*, which is just unique in that network
	- When the device need to access the Internet, it need NAT to translate Private to one Public IP address

- **NAT (Network Address Translation)**: *translate Private IP address to one Public IP address* and vice versa
	- e.g., look at the image

- **Static vs Dynamic IP**: 
	- Static: when the user assign an IP manually
	- Dynamic: get from the DHCP server

- **DHCP (Dynamic Host Configuration Protocol)**: give IP address to the host
	- Include IP address, subnet mask, Default gateway, DNS server
	- Runs in *the server* (ISP) or *the router* (home)
	- Has a *pool* of limited IP address (4 billions with DHCP from the ISP, and *depends on the subnet mask* in home network)
	- **Lease**: the amount of *time* a host can use that IP address
		- If the time limit has met, the device needs to *verify* it is still online to continue using that IP
		- If not, that IP will be given to something else
		- e.g., if the time limit is 1:10 PM, when that time comes, the computer needs to send a signal to verify its existence
		- If the device use a static IP, that IP will not be given to something else

- Basically, in your house, DHCP gives devices IP addresses, and when they need to access the Internet, NAT translate that Private IP to one Public IP

- If you want a Static + Public IP address, you gotta buy it (expensive AF)

- Your home public IP is Dynamic too


## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/305)