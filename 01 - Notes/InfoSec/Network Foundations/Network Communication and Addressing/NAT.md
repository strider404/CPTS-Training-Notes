
2025-06-16 12:16

Tags: 

## Network Address Translation (NAT)

#### IP Address Types

- **Public IP Addresses**: Globally unique addresses assigned by Internet Service Providers (ISPs). They are routable on the internet, allowing direct communication between devices across the globe.

- **Private IP Addresses**: Non-routable addresses used within local networks (e.g., homes, offices). They are defined by RFC 1918 and fall within specific ranges (e.g., `192.168.0.0/16`). These addresses are not visible on the public internet.

#### NAT

- **Network Address Translation (NAT)** is a *process* used by routers to allow *multiple devices on a private network to share a single public IP address*.

- **How it works**:
	- A device on a private network (e.g., with IP `192.168.1.10`) sends an outgoing request to the internet.
	- The router receives this request and *replaces the device's private source IP address with its own public IP address* (e.g., `203.0.113.50`).
	- The router keeps a record of this mapping in a *NAT table*, often including *port* numbers to distinguish between multiple internal devices.
	- When a response comes back to the router's public IP, the router uses the *NAT table* to identify the original internal device and forwards the packet to it by *translating the destination IP back to the private address*.

![[Pasted image 20250616124844.png]]


#### Types of NAT

- **Static NAT**: A *one-to-one* mapping where a specific private IP address is *permanently* mapped to a specific public IP address.

- **Dynamic NAT**: A private IP address is mapped to a public IP address from a pool of *available public IPs*. The mapping is *temporary* and assigned on demand.

- **Port Address Translation (PAT) / NAT Overload**: Multiple private IP addresses are mapped to a single public IP address. *Connections are differentiated by using unique port numbers*. This is the most common type used in home and small office networks.

#### Benefits and Trade-Offs

- **Benefits**:
    - Conserves the finite IPv4 address space.
    - Enhances security by hiding the internal network structure from the public internet.
    - Provides flexibility for managing internal IP addressing schemes.
- **Trade-Offs**:
    - Breaks the principle of end-to-end connectivity, which can affect certain protocols.
    - Complicates hosting services (e.g., web servers) on the private network, requiring extra configurations like port forwarding.
    - Adds a layer of complexity to network troubleshooting.
## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3240)