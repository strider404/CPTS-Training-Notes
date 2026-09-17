
2025-05-27 22:02

Tags: #network  

## TCP/UDP Connections

- Both **Transmission Control Protocol (TCP)** and **User Datagram Protocol (UDP)** are *fundamental* for sending information online.

- *TCP (Connection-Oriented):*
	- Used for **important data** like web pages and emails.
	- Ensures **all data is received** by establishing a connection, similar to a phone call.
	- Features **error recovery**: if data is lost, the receiver requests the sender to resend it.
	- This makes TCP **reliable but slower** due to the overhead of connection management and error checking.

- *UDP (Connectionless):*
	- Used when **speed is prioritized over reliability**, such as for streaming video or online gaming.
	- **No verification** that data is complete or error-free.
	- If data is lost, it's **not resent**.
	- This makes UDP **faster but potentially lossy**.

## IP Packet

- **Internet Protocol (IP) packet** is the data transmitted between computers at the *Layer 3 (network layer)* of the OSI model.

- *Structure*:
	- **Header** (routing and protocol information)
	- **Payload** (the actual data)

#### IP header

| **Field**                | **Description**                                                                  |
| ------------------------ | -------------------------------------------------------------------------------- |
| `Version`                | Indicates which *version* of the IP protocol is being used                       |
| `Internet Header Length` | Indicates the *size* of the header in 32-bit words                               |
| `Class of Service`       | Means how *important* the transmission of the data is                            |
| `Total length`           | Specifies the total *length* of the packet in bytes                              |
| `Identification (ID)`    | Is used to identify *fragments* of the packet when fragmented into smaller parts |
| `Flags`                  | Used to *indicate fragmentation*                                                 |
| `Fragment Offset`        | Indicates *where the current fragment* is placed in the packet                   |
| `Time to Live`           | Specifies how *long* the packet may *remain* on the network                      |
| `Protocol`               | Specifies which *protocol* is used to transmit the data, such as TCP or UDP      |
| `Checksum`               | Is used to detect *errors* in the header                                         |
| `Source/Destination`     | Indicate where the packet was sent *from* and where it is being sent *to*        |
| `Options`                | Contain *optional* information for routing                                       |
| `Padding`                | *Pads* the packet to a full word length (multiple of 32 bits)                    |

- If a computer has *multiple IP addresses*, the **ID** for packets sent from that computer will be different for each packet but will often be sequential or very similar.

- Example:

![[Pasted image 20250527221554.png]]

- These packets are from 2 IP addresses but the ID is *sequential* => from the same host

#### IP Record-Route Field

- **Record-Route Field**: An *option* in the IP header that **records the route** (IP addresses of intermediate routers) a packet takes to a destination.

- When a `ping` with the Record Route option (`-R`) is sent, the destination device sends back an [*ICMP Echo Reply*](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FProtocols%20%26%20Terminologies%2FCommon%20Protocols), and the **Record-Route field** in the IP header of this reply lists the IP addresses of devices the packet traversed.

![[Pasted image 20250527222242.png]]

- **Route Tracing Tool:** Used to trace the path to a destination more accurately than just `ping -R`. Use the TCP Timeout Method

- **TCP Timeout Method**
	- Sends a **TCP SYN packet** to the destination with a **TTL of 1**.
	- If TTL > 1:
		- The router **decrements the TTL value by 1**.
		- The packet is then **forwarded** to the next hop (device) in the path towards its destination.
	- If TTL = 1:
		- The router **drops (discards) the packet**.
		- The router then sends an **ICMP "Time Exceeded" message** back to the original sender of the TCP SYN packet.
	- The first router *decrements TTL to 0,* drops the packet, and sends an **ICMP Time-Exceeded** message back to the source. The source notes this router's IP.
	- The source sends another TCP SYN packet with **TTL incremented by 1**.
	- This process repeats, incrementing TTL each time, *until the TCP SYN packet reaches the destination host.*
	- The destination responds with a **TCP SYN/ACK** (if the port is open) or **TCP RST** (if the port is closed), indicating the route has been traced.

#### IP Payload

- Aka **IP Data**, this is the content being transmitted, carrying data from upper-layer protocols like TCP or UDP. It's the "letter" inside the "envelope."


## TCP Segments

- *TCP packets (segments)* have a **header** and a **payload**, and these segments are encapsulated within IP packets.

- *TCP Header Fields*:
	- **Source Port:** Sender's port number.
	- **Destination Port:** Recipient's port number.
	- **Sequence Number:** Order of data bytes.
	- **Acknowledgment (Confirmation) Number:** Confirms receipt of data.
	- **Control Flags (e.g., SYN, ACK, FIN, RST, PSH, URG):** Manage connection state and data flow.
	- **Window Size:** How much data the receiver can accept.
	- **Checksum:** Error detection for header and payload.
	- **Urgent Pointer:** Indicates important data in the payload.

- *TCP Payload*: The actual application data being transmitted.


## UDP Datagrams

- UDP transfers *datagrams* (small data packets)

- **Connectionless:** Does **not** establish a connection before sending data; data is sent directly.

- When `traceroute` uses UDP, and the UDP datagram reaches the target device, an **ICMP "Destination Unreachable" (Type 3), "Port Unreachable" (Code 3)** message is typically sent back.


## Blind Spoofing

- **Data Manipulation Attack:** An attacker sends **false information** (spoofed packets) onto a network **without seeing the actual responses** from target devices.

- **Mechanism:** Involves manipulating IP header fields, such as:
	- **False source and destination addresses.**
	- **False Initial Sequence Number (ISN)** in TCP headers. The ISN is set by the sender in the first packet of a TCP connection.

- Why it is *"blind"*:
	- The attacker sends packets with a **fake (spoofed) source IP address**. This *isn't their real IP*.
	- So the victim sends its replies **to that fake IP address**
	- =>The attacker *cannot directly know* if their spoofed packet was successful or what the target did in response

- **Goal:** Can cause a target host to establish a connection with the attacker (or a non-existent host) or interact based on falsified information.

- **Uses:**
    - Disrupting network connection integrity.
    - Breaking connections between devices.
    - Monitoring network traffic (less common with _blind_ spoofing, as responses aren't seen directly).
    - Intercepting information (similarly, challenging with pure blind spoofing).

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1879)