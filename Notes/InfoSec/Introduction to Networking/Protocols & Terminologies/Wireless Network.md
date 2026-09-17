
2025-05-18 21:52

Tags: #network  

## Wireless Network

- Wireless networks using **radio frequency (RF)** technology

- Each device on a wireless network has a *wireless adapter* that converts RF to useable form and vice versa

- **Technologies**:
	- LAN: WiFi
	- WWAN: cellular data (3G, 4G LTE, 5G)

- **Bands**: 2.4GHz or 5GHz

- Devices (phone, laptop) needs to communicate with the **Wireless Access Point (WAP) (router)** to send data to another WAP then to the other devices

## WiFi Connection

- To *connect to the router*, devices need to use **IEEE 802.11**, which defines how devices associate with WAPs
	- Devices need to send *connection request frame* to the router, include:
		- **MAC Address**
		- **SSID (network name)**
		- **Supported Data Rates**
		- **Supported channels (frequency)**
		- **Security Protocols (WPA2/WPA3)**

- The WAP processes these and, upon validation, grants network access.

## Security Features

- **Encryption**: common algorithms:
	- Wired Equivalent Privacy (*WEP*)
	- WiFi Protected Access 2 (*WPA2*)
	- WiFi Protected Access 3 (*WPA3*)

- **Access Control**: 
	- Default: allow authorized devices to join the network using specific authentication methods
	- can be changed (like allow specific MAC)

- **Firewall**: *controls incoming and outgoing network traffic* based on predetermined security rules
	- Router too, has its own firewall


## Encryption Protocols

- 2 main types of **algorithms**
	- WEP
	- WPA

#### WEP
- **WEP (Wired Equivalent Privacy)** employs a **challenge-response handshake** between a WAP and a client device

|**Step**|**Who**|**Description**|
|---|---|---|
|1|`Client`|Sends an association request packet to the WAP, requesting access.|
|2|`WAP`|Responds with an association response packet to the client, which includes a challenge string.|
|3|`Client`|Calculates a response to the challenge string and a shared secret key and sends it back to the WAP.|
|4|`WAP`|Calculates the expected response to the challenge with the same shared secret key and sends an authentication response packet to the client.|
- **Cyclic Redundancy Check (CRC)** is used to ensure the integrity of data (because some might be lost in transmission)
	- Has a flaw that can be decrypted without secret key (because it is created in plaintext)

- WEP uses the **RC4** cipher encryption algorithm (kinda vulnerable vs the AES)

- Has 2 **version**:
	- `WEP-40`/`WEP-64` (40-bit secret key)
	- `WEP-104` (80-bit secret key)

- **Key components**:
	- *Initialization Vector (IV)*
		- It ensures that the *same plaintext* data encrypted multiple times yields *different ciphertexts*
		- It is the main difference of the keys of the sender/recipient 
	- *Secret key*
		- A shared *static* key configured manually on both the access point and the client.

| **Protocol**      | **IV** | **Secret Key** |
| ----------------- | ------ | -------------- |
| `WEP-40`/`WEP-64` | 24-bit | 40-bit         |
| `WEP-104`         | 24-bit | 104-bit        |

- The IV is kinda small, so we can brute force it

#### WPA

- **WPA** provides the highest level of security

- Using AES (Advanced Encryption Standard)


## Authentication Protocols

- **2 main protocols**:
	- Lightweight Extensible Authentication Protocol (**LEAP**)
	- Protected Extensible Authentication Protocol (**PEAP**)
	- Both uses the Extensible Authentication Protocol (EAP)

- Both uses the Extensible Authentication Protocol (EAP), uses in many context

- **LEAP** uses a *shared key* for authentication, which means that the *same* key is used for encryption and authentication

- **PEAP** uses *Transport Layer Security (TLS)*, 
	- Establishes a secure connection between the device and the WAP using a `digital certificate`, and an encrypted tunnel protects the authentication process

- **TACACS+ (Terminal Access Controller Access-Control System Plus)**: a protocol used to *authenticate* and *authorize* users accessing network devices, such as routers and switches
	- Encrypt entire request packet
	- Used in enterprises

## Wireless Attacks and Countermeasures

- **Disassociation Attack**: Sends spoofed disassociation frames to *disconnect* users, possibly leading to **Man-in-the-Middle (MITM)** attacks.

- **Wireless Hardening Techniques**:
	- Disabling Broadcasting
	- WPA
	- MAC Filtering
	- Deploying EAP-TLS


## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1873)