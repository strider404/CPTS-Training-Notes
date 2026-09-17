
2025-06-23 17:31

Tags: #network  

## TCP/IP Model vs OSI Model

- [TCP/IP](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetwork%20Workflow%2FThe%20TCP%20IP%20Model)

- [OSI](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetwork%20Workflow%2FThe%20OSI%20Model)

- TCP/IP is more practical, while OSI is more theoretical about how things work

#### PDU

- **PDU (Protocol Data Unit):** A data packet containing *control information* and data from each layer of a networking model.

- **Encapsulation:** The process where data moving down the protocol stack is *wrapped* by each layer. *Each layer adds a header with necessary information* (e.g., source/destination addresses, ports, protocol flags).

![[Pasted image 20250623174341.png]]

- *PDU breakdown (reverse order):*

![[Pasted image 20250623174249.png]]


## Addressing Mechanisms

![[Pasted image 20250623221216.png]]


- *MAC* (Media Access Control) Address - **RED Arrow**
	- [Elaborate](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FAdressing%2FMAC%20Address)
	- When a packet needs to cross a router (a Layer 3 device), the router *strips* the Layer 2 encapsulation and *re-encapsulates it with the MAC address of the next hop.*

- *IP* (Internet Protocol) Address - **GREEN Arrow**
	- [Elaborate](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FAdressing%2FIP%20Address)

- *IPv6* (Internet Protocol version 6) - **BLUE Arrow**
	- [Elaborate](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FAdressing%2FIPv6%20Addresses)

## TCP / UDP, Transport Mechanisms

- **TCP (Transmission Control Protocol)**
    - **Connection-Oriented:** Establishes a *formal connection* before data transfer.
      
    - **Reliable:** Uses a three-way handshake, sequence numbers, and acknowledgments (ACKs) to *guarantee* data delivery and order.
      
    - **Slower:** The overhead from its reliability features makes it *slower* than UDP.
      
    - **Use Cases:** Situations where data integrity is critical (e.g., SSH, file transfers, web Browse).


- **UDP (User Datagram Protocol)**
    - **Connectionless:** "Fire and forget" protocol; *no connection* is established.|
      
    - **Unreliable:** *Does not guarantee* delivery, order, or error checking.
      
    - **Faster:** Minimal overhead makes it very *fast*.
      
    - **Use Cases:** Speed-sensitive applications where minor data loss is acceptable (e.g., video streaming, online gaming, DNS queries).


## TCP Three-way Handshake

- **Three-Way Handshake** (Connection Establishment)
	- **Client -> Server:** Sends a packet with the *SYN* (synchronize) flag set.
	  
	- **Server -> Client:** Responds with a packet containing both *SYN* and *ACK* (acknowledgment) flags.
	  
	- **Client -> Server:** Sends a final packet with the *ACK* flag set, establishing the connection.


- *Session Teardown* (Graceful Connection Closure)
	- **Client -> Server:** Sends *FIN, ACK* to request termination.
    
	- **Server -> Client:** Sends its own *FIN, ACK* when it is ready to close.
    
	- **Client -> Server:** Sends a final *ACK* to close the connection completely.

## References:

[Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/81/section/954)