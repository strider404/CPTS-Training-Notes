
2025-06-16 10:38

Tags: #network  

## End Devices

- **End Devices:** Devices that *send or receive data* and serve as the *user interface* to the network.

- **Examples:** Computers, smartphones, tablets, IoT devices.

- **Function:** Generate and consume data, allowing users to access network services like Browse the web or sending messages.

## Intermediary Devices

- **Intermediary Devices:** Devices that *facilitate data flow* and *manage traffic* between end devices and networks.

#### Network Interface Cards (NICs)

- **Network Interface Card (NIC)**: a *hardware* component that *enables a computer to connect to a network*

- Each NIC has a *unique* Media Access Control (*MAC*) address

- Can be designed for Wired/Wireless

- Example: Realtek PCIe GbE Family Controller

![[Pasted image 20250616104952.png]]

![[Pasted image 20250616105006.png]]


#### Routers

- **Routers (OSI Layer 3):** Forward data packets _between different networks_ using *IP addresses* and *routing protocols* (e.g., OSPF, BGP).

#### Switches

- **Switches (OSI Layer 2):** Connect devices _within the same local network (LAN)_, forwarding data to specific recipients using *MAC addresses*.

#### Hubs

- **Hubs (OSI Layer 1):** Antiquated devices that connect multiple devices by *broadcasting* data to all ports, leading to *inefficiency*.


## Network Media and Software Components

- **Network Media and Software Components:** The *physical* and *logical* elements that enable network communication.

#### Network Media

- **Network Media:** The physical pathways for data transmission.

- **Examples:** Wired (Ethernet, fiber-optic cables) and wireless (Wi-Fi, Bluetooth).

#### Network Protocols

- **Network Protocols:** A set of rules governing how data is formatted, transmitted, and received.

- **Examples:** TCP/IP (internet), HTTP/HTTPS (web), FTP (file transfer).

#### Network Management Software

- **Network Management Software:** Tools used by administrators to monitor, configure, and maintain network performance and security.

#### Software Firewalls

- **Software Firewalls:** Security applications installed on individual end devices (hosts) to *control incoming and outgoing traffic* *based on specific rules*.


## Servers

- **Servers:** Powerful computers that provide services and resources to other computers (clients) on the network.

- **Function:** Host websites, manage files, handle email, store data, and authenticate users.

- **Model:** Operates on the "Client-Server Model," where servers respond to requests from clients.

## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3237)