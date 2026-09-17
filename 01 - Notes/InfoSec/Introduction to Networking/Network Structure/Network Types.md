
2025-04-24 12:09

Tags: #network  

## Common Terminology

| **Network Type**                       | **Definition**                                 |
| -------------------------------------- | ---------------------------------------------- |
| Wide Area Network (**WAN**)            | Internet                                       |
| Local Area Network (**LAN**)           | Internal Networks (Ex: Home or Office)         |
| Wireless Local Area Network (**WLAN**) | Internal Networks accessible over Wi-Fi        |
| Virtual Private Network (**VPN**)      | Connects multiple network sites to one **LAN** |

- **WAN**: large-scale networks connecting multiple LANs (not exclusively be the Internet)
	- Identified by **public IPs** and **WAN routing protocols** (e.g., BGP).

- **LAN**: Internal network, typically uses **private IP ranges** (RFC 1918).

- **WLAN (Wireless LAN):** LAN with wireless (Wi-Fi) capability, functionally the same as LAN but with wireless access.

- **VPN**: making the user feel as if they were plugged into a different network -> more secured network
	- **Site-to-Site VPN**: ==connects multiple networks== securely, allowing them to share resources as if they were part of a ==single, unified== network
	- **Remote Access VPN:** Makes a ==client device== create a virtual interface that ==behaves as if it is on a remote network.==
	- **Split-tunnel VPNs** only route ==specific traffic through the VPN==, while ==other traffics== go to the Internet as usual


## Book Terms

| **Network Type**                          | **Definition**                                        |
| ----------------------------------------- | ----------------------------------------------------- |
| Global Area Network (**GAN**)             | Global network (the Internet)                         |
| Metropolitan Area Network (**MAN**)       | Regional network (multiple LANs), like a city network |
| Wireless Personal Area Network (**WPAN**) | Personal network (Bluetooth)                          |
## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/298)