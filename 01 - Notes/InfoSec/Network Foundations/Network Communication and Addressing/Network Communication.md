
2025-06-16 11:24

Tags: #network  

## MAC Addresses

- **MAC (Media Access Control) Address:** A *unique, permanent hardware identifier* assigned to a *Network Interface Card (NIC)*.

- **OSI Layer:** Operates at *Layer 2* (Data Link).

- **Usage:** Essential for communication _within_ a local area network (LAN). *Switches* use MAC addresses to forward *data frames* to the correct physical device.

- **Format:** A 48-bit number shown as six pairs of hexadecimal digits (e.g., `00:1A:2B:3C:4D:5E`).
	- The first 24 bits are the **Organizationally Unique Identifier (OUI)**, which identifies the manufacturer.
	- The last 24 bits are *unique* to the specific device.

- **Key Protocol:** The **Address Resolution Protocol (ARP)** maps IP addresses (Layer 3) to MAC addresses (Layer 2) on a local network.


## IP Addresses

- **IP (Internet Protocol) Address**: A logical, numerical label assigned to a device on a network.

- **OSI Layer:** Operates at *Layer 3* (Network).

- **Usage:** Enables communication _across_ different networks. *Routers* use IP addresses to determine the optimal path for *data packets*.

- **Assignment:** Unlike MAC addresses, IP addresses can be *dynamic* and change based on the network configuration.

- **Versions:**
    - **IPv4:** A 32-bit address (e.g., `192.168.1.1`).
    - **IPv6:** A 128-bit address created to overcome the limitation of IPv4 addresses (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).

## Ports

- **Ports**: a *number assigned to specific processes or services* on a network to help computers sort and direct network traffic correctly

- Allowing a *single IP address* to handle multiple network services simultaneously.

- **OSI Layer:** Operates at *Layer 4* (Transport), working alongside protocols like TCP and UDP.

- **Usage:** Sorts and directs network traffic *to the correct application*

- **Categories (Range 0-65535):**
	- **Well-Known Ports (0-1023):** Reserved by IANA for *standard, universal services* (e.g., FTP on 20/21, HTTP on 80, HTTPS on 443).
	- **Registered Ports (1024-49151):** Registered with IANA for *specific applications* to avoid conflicts (e.g., Microsoft SQL Server on 1433).
	- **Dynamic/Private Ports (49152-65535):** Used for *temporary, short-term* communication sessions, typically assigned *randomly* by the client's operating system.

#### Example: Browse the Internet

- **DNS Lookup:** Your computer resolves a domain name (e.g., `example.com`) into an IP address (e.g., `93.184.216.34`).

- **Data Encapsulation:** Your browser creates an HTTP request, which is encapsulated with a TCP header specifying the destination **port** (80 or 443) and the destination **IP address**.

- **Local Transmission:** Your computer uses *ARP* to find the **MAC address** of the local network's default gateway (router) to send the data packet out.

- **Routing & Server Processing:** Routers forward the packet across the internet based on the destination **IP address**. The receiving server gets the packet and, based on the **port** number, *directs it to the web server application*.

- **Response:** The server sends a response back to your computer's **IP address** and the temporary **dynamic port** that your OS assigned for the session.

## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3238)