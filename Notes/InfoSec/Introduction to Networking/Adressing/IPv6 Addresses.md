
2025-05-14 10:37

Tags: #network  

## IPv6 Addresses

- [Last lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FIP%20Address)

- **IPv6** is the successor to **IPv4**, offering a **128-bit** (16 bytes) address space (vs. IPv4's 32-bit), managed by **IANA**.

- Designed to **replace IPv4**, though both can coexist via **Dual Stack**.

- Adheres to the **end-to-end principle**, removing the need for NAT (cause now you never run out of IP addresses) and enabling **multiple addresses per interface**.

- **Has 2 parts**:
	- **Network Prefix (Network part)**: Identifies *network/subnet* (default is /64, but can be changed)
	- **Interface Identifier or Suffix (Host part)**: Typically *derived* from the device’s *MAC* address, expanded to 64 bits.

- **Types**:

|**Type**|**Description**|
|---|---|
|`Unicast`|Addresses for a single interface.|
|`Anycast`|Addresses for multiple interfaces, where only one of them receives the packet.|
|`Multicast`|Addresses for multiple interfaces, where all receive the same packet.|
|`Broadcast`|Do not exist and is realized with multicast addresses.|

- Can use double-colon to express one or more blocks of 0:
	- Full: `fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64`
	- Short: `fe80::dd80:b1a9:6687:2d3b/64`

- RFC 5952 Formatting Rules
	- Use **lowercase letters**.
	- **Omit leading zeros** in each block.
	- Use `::` **once** to replace the **longest** sequence of zero blocks.

## IPv4 vs IPv6 Comparison

| **Feature**        | **IPv4**        | **IPv6**                 |
| ------------------ | --------------- | ------------------------ |
| *Bit length*         | 32-bit          | 128-bit                  |
| *Address format*     | Binary          | Hexadecimal              |
| *Addressing range*   | ~4.3 billion    | ~340 undecillion         |
| *Prefix notation*    | `10.10.10.0/24` | `fe80::dd80:...:2d3b/64` |
| *Dynamic addressing* | DHCP            | SLAAC / DHCPv6           |
| *IPsec*              | Optional        | Mandatory                |
| *OSI Layer*          | Network Layer   | Network Layer            |

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/482)