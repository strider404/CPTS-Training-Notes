
2025-05-05 15:58

Tags: #network  

## Subnetting

- [Last lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FIP%20Address)

- **Subnetting** is the process of **dividing a large IPv4 address block** into smaller addresses (subnets).

- Each subnet has its ==own== network address, broadcast address and host addresses

- **Network part / Host part**:
	- IPv4 Address: `192.168.12.160`
	- Subnet Mask: `255.255.255.192`
	- CIDR: `192.168.12.160/26` (26 bits are from network part)
	- -> Network part | Host part: **1100 0000 1010 1000 0000 1100 10**==10 0000==

- The **network part is fixed**, while the host part can be changed

- **Network address** is where all the bits in host part are 0: **1100 0000 1010 1000 0000 1100 10**==00 0000== -> 192.168.12.128

- **Broadcast address** is where all the bits in host part are 1: **1100 0000 1010 1000 0000 1100 10**==11 1111== ->192.168.12.191

- **Host address** are addresses between Network and Broadcast

## Subnetting Into Smaller Networks

- **Can only divided into 2^n subnets**

- Extend the Network part by n bits

- e.g., Divide into 4 subnet 192.168.12.128/26 -> extend the mask by **2 bits** → /28:
	- Each subnet = 16 addresses (14 usable)
	- Resulting subnets:

| **Subnet** | **Network Address** | **First Host** | **Last Host**  | **Broadcast Address** |
| ---------- | ------------------- | -------------- | -------------- | --------------------- |
| 1          | 192.168.12.128/28   | 192.168.12.129 | 192.168.12.142 | 192.168.12.143        |
| 2          | 192.168.12.144/28   | 192.168.12.145 | 192.168.12.158 | 192.168.12.159        |
| 3          | 192.168.12.160/28   | 192.168.12.161 | 192.168.12.174 | 192.168.12.175        |
| 4          | 192.168.12.176/28   | 192.168.12.177 | 192.168.12.190 | 192.168.12.191        |

- **Quickly calculate** subnet size:
	- Size = 2^(32-CIDR) address

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/306)
