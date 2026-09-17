
2025-06-19 11:14

Tags: #network  

## Data Flow Example

![[Pasted image 20250619113008.png]]

#### Network Connection and Configuration

- The client PC connects to the local Wireless LAN (*WLAN*), authenticating with credentials if required.

- The PC sends a *DHCP IP Request* to the router to obtain network configuration details.

- The router's DHCP server responds with a *DHCP IP Response*, assigning the PC a private IP address (e.g., `192.168.1.10`), subnet mask, default gateway (the router's IP), and a DNS server address.

#### Domain Name System (DNS) Resolution

- - The PC sends a *DNS Query* for the target domain (e.g., `www.example.com`) to the DNS server provided by the DHCP configuration.

- The router forwards this query to the public DNS server.


- The DNS server replies with a *DNS Response* containing the public IP address of the web server (e.g., `93.184.216.34`).

#### HTTP Request and Encapsulation

- **Application Layer:** The browser creates an *HTTP* (or HTTPS) *request* for the webpage.

- **Transport Layer:** The request becomes a *TCP segment* with source and destination *port* numbers (e.g., destination port 80 for HTTP).

- **Internet Layer:** The segment is placed into an *IP packet* with the source set to the PC's private *IP* and the destination as the web server's public IP.

- **Link Layer:** The packet is put into a *frame* with the PC's *MAC* address as the source and the router's MAC address as the destination.

#### Request Forwarding and NAT

- The PC sends the request frame to the *router*.

- The router performs **Network Address Translation (NAT)**, replacing the PC's private source IP address in the packet with its own public IP address.

- The router forwards the modified packet onto the internet, where it is routed to the destination web server.

#### Server Processing and HTTP Response

- The web server receives the *HTTP Request*.

- It processes the request and generates an *HTTP Response* containing the webpage's content (HTML, CSS, etc.).

- This response packet is addressed from the web server's IP to the router's public IP.

#### Response Return and Rendering

- The response travels back across the internet to the router.

- The router uses its NAT table to map the response back to the original PC, *replacing* the destination public IP with the PC's private IP.

- The PC receives the packet, decapsulates it, and the browser engine reads the content to *render the webpage*.


## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3245)