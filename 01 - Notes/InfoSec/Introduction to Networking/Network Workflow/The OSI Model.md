
2025-04-29 11:22

Tags: #network  

## Layers

- [Last lesson](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FIntroduction%20to%20Networking%2FNetworking%20Models)

- A 7-layer *conceptual framework* that standardizes network functions.

| **Layer** | **Name**         | **Function Summary**                                                                                                         |
| --------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 7         | **Application**  | Provides network services directly to *end-user applications* (e.g., HTTP, FTP).                                             |
| 6         | **Presentation** | *Encrypts, decrypts*, and compresses data, make sure info from this application can be read by the other                     |
| 5         | **Session**      | Establishes, manages, and terminates *connections between applications* (e.g., APIs).                                        |
| 4         | **Transport**    | Manages *end-to-end communication*, reliability, and *flow control* (e.g., TCP, UDP).                                        |
| 3         | **Network**      | Handles *packet forwarding* and routing across networks using *IP addresses* (e.g., routers), *different network*            |
| 2         | **Data Link**    | Provides *node-to-node* (direct link between 2 devices) data transfer using *MAC addresses* (e.g., switches), *same network* |
| 1         | **Physical**     | *Transmits raw bitstreams* via physical hardware (e.g., cables, waves).                                                      |
- **Layers 1–4**: Focused on **data transport** (reliability, routing, transmission).

- **Layers 5–7**: Focused on **application-level interactions**.

- When data is transferred, it involves all 7 layers on both ends

- ==Main differences== with the TCP/IP: Layer 6, 5; 2, 1. Also OSI is more referenced in technical environment, while TCP/IP is used more in day-to-day life

![[Pasted image 20250613213749.png]]

## Operation Flow

- **Sending side:** Data flows **from Layer 7 (Application) down to Layer 1 (Physical)**.

- **Receiving side:** Data is **unwrapped from Layer 1 up to Layer 7**.

- Each layer **adds or removes headers**, depending on the direction of flow.


## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/302)
