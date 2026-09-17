
2025-04-25 17:18

Tags: #network  

## Proxies

-  **Proxy**:  a **device or service** sits in the ==middle== of a connection and acts as a ==mediator==.
	- **Mediator**: ==be able to inspect the content==
	- If it cannot -> it's a **gateway**

- Proxies will almost always operate at **Layer 7 of the OSI Model**

- **Types**:
	- Dedicated Proxy / Forward Proxy
	- Reverse Proxy
	- Transparent Proxy

## Dedicated Proxy / Forward Proxy

- **Definition**: Sits ==between a client and the internet==, handling **outgoing** requests on the client’s behalf.

- **Use Case**: Common in corporate environments to control internet access and ==defend against malware.==
	- If the malware wants to bypass the proxy, it needs to be **proxy aware**

- **Tool**: **Burp Suite**, typically used to forward HTTP requests but can be configured for other proxy types too.

![[Pasted image 20250425173004.png]]


## Reverse Proxy

- **Definition**: Sits ==between the internet and a backend server==, handling **incoming** requests (from the server behalf) and **forwarding** it to a closed-off network.

- **Use Case**: Protects internal servers, often used for load balancing, DDoS protection, or masking internal infrastructure.

- **Pentesting Use**: Used to tunnel traffic through infected machines to evade firewalls or IDS/IPS by leveraging reverse proxies over compromised endpoints (e.g., via SSH tunnels).

- **Common Tools**: **Cloudflare** and **ModSecurity (WAF)**, which inspect or block malicious inbound traffic.

![[Pasted image 20250425174720.png]]

## Transparent vs Non-Transparent Proxies

- Above proxies is either one of these

- **Transparent Proxy**: Operates without client awareness; traffic is intercepted silently.

- **Non-Transparent Proxy**: Requires explicit configuration on the client; without it, internet access is usually blocked.

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/300)