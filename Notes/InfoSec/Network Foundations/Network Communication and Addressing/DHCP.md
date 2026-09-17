
2025-06-16 12:06

Tags: #network  

## Dynamic Host Configuration Protocol (DHCP)

- **DHCP**: a network management *protocol* that **automates the assignment of IP addresses** and other network configuration parameters (e.g., subnet mask, default gateway, DNS servers) to devices on a network.

- It simplifies network administration, prevents IP address conflicts, and optimizes the use of the available IP address pool.

- **Core Components**:
	- **DHCP Client**: Any device on the network that requests configuration information.
	- **DHCP Server**: A router or dedicated server that manages a pool of IP addresses and responds to client requests.

#### The DORA Process

- The *four-step* process for a client to obtain an IP address:
	- **Discover**: A client connects to the network and broadcasts a `DHCP Discover` message to find any available DHCP servers.
	- **Offer**: DHCP servers respond with a `DHCP Offer` message, proposing an IP address and other parameters to the client.
	- **Request**: The client selects an offer and sends a `DHCP Request` message back to the server, formally asking to use the offered IP address.
	- **Acknowledge**: The server finalizes the transaction by sending a `DHCP Acknowledge` message, confirming the IP address assignment to the client.


#### IP Address Leasing

- IP addresses assigned by DHCP are *not permanent*; they are "leased" for a specific period known as the **lease time**.

- Before the lease expires, the client must *send a renewal DHCP Request* to the DHCP server to continue using the IP address.

- The server can then acknowledge the request, *extending* the lease.

![[Pasted image 20250616121431.png]]

## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3239)