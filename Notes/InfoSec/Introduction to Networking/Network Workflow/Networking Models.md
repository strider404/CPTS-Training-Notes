
2025-04-29 10:25

Tags: #network  

## Networking Models

![[Pasted image 20250429102618.png]]

## OSI Model

- **OSI - ISO/OSI model (Open Systems Interconnection)**: 7 layers

- Published by **International Organization for Standardization (ISO)**


## TCP/IP Model

- **TCP/IP (Transmission Control Protocol/Internet Protocol)**: a ==generic term== for an entire protocol family (not just 2 protocols)
	- **ICMP (Internet Control Message Protocol)**/ **UDP (User Datagram Protocol)**/**TCP**/**IP** also belong to this family

- 4 layers

## ISO/OSI vs. TCP/IP

- **TCP/IP**: a set of communication ==protocols== that ==allows hosts to connect to the Internet==

- **OSI**: a ==conceptual framework== between the network and end-users
	- Is a reference model: because it abstracts how data is transferred in the Internet, it is a blueprint, but not directly implemented irl

- **TCP/IP** is **implementation-driven**, and **flexible**.

- **OSI** aimed for **academic purity**, defining **strict modular separation** between layers

- OSI became the **idealized** model; TCP/IP became the **practical** reality


## Packet Transfer

- **Protocol Data Units (PDUs)** are the formatted data exchanged at each layer

- As data moves **downward from application to physical layer**, each layer **adds a header** to the PDU—this is ==encapsulation==.
	- e.g., in the image below, the Transport layer adds a **TCP header** to the data, the *Internet Layer* adds an *IP header*,...

![[Pasted image 20250429110859.png]]


- ==Decapsulation==: On the ==receiving== side, data is **unpacked layer-by-layer**, **headers are processed/removed**, and finally the clean data reaches the application.
	- e.g., Link Layer converts bits into a **Frame**, then removes the **MAC header**, Internet Layer Removes the **IP header**, leaving TCP + Data,... 
## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/301)