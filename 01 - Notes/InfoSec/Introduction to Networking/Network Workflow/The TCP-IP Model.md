
2025-04-29 13:43

Tags: #network  

## The TCP/IP Model

- [Last lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetwork%20Workflow%2FNetworking%20Models)

- **TCP/IP** (or **Internet Protocol Suite**): a **four-layered reference model** that defines protocols used for communication across interconnected networks such as the Internet

- Named after 2 core protocols: **Transmission Control Protocol (TCP)** and **Internet Protocol (IP)**.

| **Layer**       | **Function**                                                                                                                                                                                                                                                                            |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `4.Application` | ==Interfaces== with software apps; defines data ==exchange protocols== like HTTP, FTP, etc. (OSI Layers 5, 6, & 7).                                                                                                                                                                     |
| `3.Transport`   | Providing ==reliable== (TCP) or ==fast== (UDP) data transmission and session management. (OSI Layer 4).                                                                                                                                                                                 |
| `2.Internet`    | Handles ==IP addressing, routing, and packet forwarding== across networks. (OSI Layer 3).                                                                                                                                                                                               |
| `1.Link`        | The Link layer is responsible for ==placing the TCP/IP packets on the network medium (physical)== and ==receiving== corresponding packets from the network medium. TCP/IP is designed to work independently of the network access method, frame format, and medium. (OSI Layers 1 & 2). |

![[Pasted image 20250614211803.png]]


- **TCP** is in Layer 3, **IP** in Layer 2

- **Tasks**:

| **Task**                 | **Protocol** | **Description**                                                                                                                                                                                 |
| ------------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Logical Addressing**   | IP           | Structures networks using ==IP addresses== (including subnetting and CIDR).                                                                                                                     |
| **Routing**              | IP           | Determines ==optimal path== from sender to receiver across multiple nodes.                                                                                                                      |
| **Error & Flow Control** | TCP          | The sender and receiver are frequently in touch with each other via a virtual connection. Therefore ==control messages== are sent continuously to check if the connection is still established. |
| **Application Support**  | TCP/UDP      | Uses ports to ==distinguish== applications and manage multiple sessions.                                                                                                                        |
| **Name Resolution**      | DNS          | ==Resolves domain names== (FQDN) to IP addresses for easy host access.                                                                                                                          |

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/303)