
2025-06-13 17:32

Tags: #network  

## OSI Model

- [This lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetwork%20Workflow%2FThe%20OSI%20Model)

## TCP/IP Model

- [This lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetwork%20Workflow%2FThe%20TCP%20IP%20Model)

## Protocols

 - **Protocols** are *standardized rules* that determine the formatting and processing of data to facilitate communication between devices in a network.

#### Common Network Protocols

| **Protocol**                           | **Description**                                                                                                                                                                                                                      |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `HTTP (Hypertext Transfer Protocol)`   | Primarily used for *transferring web pages*. It operates at the *Application Layer*, allowing browsers and servers to communicate in the delivery of web content.                                                                    |
| `FTP (File Transfer Protocol)`         | Facilitates the *transfer of files* between systems, also functioning at the *Application Layer*. It provides a way for users to upload or download files to and from servers.                                                       |
| `SMTP (Simple Mail Transfer Protocol)` | Handles the transmission of email. Operating at the *Application Layer*, it is responsible for *sending messages* from one server to another, ensuring they reach their intended recipients.                                         |
| `TCP (Transmission Control Protocol)`  | Ensures *reliable data transmission* through error checking and recovery, operating at the *Transport Layer*. It establishes a connection between sender and receiver to guarantee the delivery of data in the correct order.        |
| `UDP (User Datagram Protocol)`         | Allows for *fast, connectionless communication*, which operates without error recovery. This makes it ideal for applications that require speed over reliability, such as streaming services. UDP operates at the *Transport Layer*. |
| `IP (Internet Protocol)`               | Crucial for *routing packets* across network boundaries, functioning at the *Internet Layer*. It handles the addressing and routing of packets to ensure they travel from the source to the destination across diverse networks.     |

## Transmission

- **Transmission** in networking refers to the process of *sending data signals* over a medium from one device to another

#### Transmission Types

- **Analog**: Uses *continuous* signals.

- **Digital**: Uses *discrete* signals (bits).

#### Transmission Modes

- **Simplex**: *One-way* communication (e.g., keyboard to computer).

- **Half-duplex**: *Two-way* communication, but not simultaneous (e.g., walkie-talkies).

- **Full-duplex**: *Simultaneous two-way* communication (e.g., telephone calls).


#### Transmission Media

- **Wired**: Twisted pair, coaxial, and fiber optic cables.

- **Wireless**: Radio waves, microwaves, and infrared.

## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3236)