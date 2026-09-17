
2025-05-19 21:45

Tags: #network 

## Virtual Private Networks

- **Virtual Private Network (VPN)**: creating a *secure, encrypted connection* between a remote device and a private network over a public network like the internet.
	- Mainly use for employees to company's private network securely

- **Benefits**:
	- *Security*: Encrypts the connection, making it difficult for attackers to intercept data.
	- *Remote Access*: Enables employees to work from home or while traveling.
	- *Cost-Effective*: Uses the public internet, which is cheaper than dedicated leased lines.
	- *Network Unification*: Connects multiple remote locations (e.g., branch offices) into a single private network

- *Requirements*:

| **Requirement**  | **Description**                                                   |
| ---------------- | ----------------------------------------------------------------- |
| `VPN Client`     | Software on the remote device.                                    |
| `VPN Server`     | A computer or device that accepts VPN connections.                |
| `Encryption`     | Algorithms like AES and protocols like IPsec.                     |
| `Authentication` | Methods like shared secrets or certificates to verify identities. |

- **Common Ports:**
	- TCP/1723 for PPTP.
	- UDP/500 for IKEv1 and IKEv2.


## IPsec

- **Internet Protocol Security (IPsec):** A *network security protocol* suite that provides encryption and authentication for internet communications.

- **IPsec is one of the primary technologies used to create and secure VPNs.**
	- Imagine VPN is the road, and the IPsec is the police to protect it

- Core Protocols:
	- **Authentication Header (AH):** Provides integrity and authenticity for IP packets but does not offer encryption.
	- **Encapsulating Security Payload (ESP):** Provides encryption and optional authentication for IP packets.

- *Modes* of Operation:
	- **Transport Mode:** *Encrypts only the data payload* of an IP packet. Typically used for end-to-end communication between two hosts.
	- **Tunnel Mode:** *Encrypts the entire IP packet*, including the header. Typically used to create a VPN tunnel between two networks.

- *Firewall Configuration for IPsec VPN*:
	- Allow **IP (UDP/50-51)**.
	- Allow **Internet Key Exchange (IKE) on UDP/500** for secure key negotiation.
	- Allow **Encapsulating Security Payload (ESP) on UDP/4500** for the encrypted data.

## PPTP

- **Point-to-Point Tunneling Protocol (PPTP):** A network protocol that creates VPNs by establishing a secure tunnel between a client and a server.

- **Security Status:** No longer considered secure due to significant, known vulnerabilities.

- **Primary Vulnerability:** Uses the MSCHAPv2 authentication method, which relies on outdated and easily crackable DES encryption.

- **Modern Relevance:** Has been largely replaced by more secure protocols such as L2TP/IPsec, IPsec/IKEv2, and OpenVPN.

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1874)
