
2025-06-16 22:00

Tags: #network  

## Internet Architecture

-  **Internet Architecture** defines how data is organized, transmitted, and managed across networks.

- Hybrid models combining different architectures are common.

## Peer-to-Peer (P2P) Architecture

- **Definition:** Each device (peer) acts as both a client and a server, *communicating directly* with others *without a central server*.

- **Example:** Torrenting (BitTorrent), where users download files from multiple other users (seeders) simultaneously.

- **Advantages:**
	- **Scalability:** Network resources increase as more nodes join.
	- **Resilience:** The network continues to function even if some nodes go offline.
	- **Cost-efficient:** Resource load (bandwidth, storage) is distributed among peers.

- **Disadvantages:**
	- **Complex Management:** Difficult to enforce updates and security policies.
	- **Unreliable:** Resources can become unavailable if peers leave the network.
	- **Security Risks:** Each node is a potential point of vulnerability.


![[Pasted image 20250617114607.png]]


## Client-Server Architecture

- **Definition:** Clients (user devices) request services and resources from *centralized servers*.

- **Example:** Browse a website, where your browser (client) requests a webpage from a web server.

- **Tiered Models**:
	- **Single-Tier:** Client, server, and database are all on *one* machine. Rarely used for large applications.
	- **Two-Tier:** Splits duties between a c*l*ient (presentation - user's interface) and a *server* (data - database).
	- **Three-Tier:** Adds an *application server* (business logic) between the client and the database server.
	- **N-Tier:** Uses *more than three tiers* for complex applications, enhancing scalability.

- **Advantages:**
    - **Centralized Control:** Easy to manage, update, and secure.
    - **Optimized Performance:** Servers can be dedicated to specific tasks.

- **Disadvantages:**
	- **Single Point of Failure:** If the central server fails, the service is unavailable.
	- **High Cost:** Expensive to set up and maintain servers.
	- **Network Congestion:** High traffic can slow down or crash the server.


## Hybrid Architecture

- **Definition:** Blends *Client-Server* and *P2P* models. A central server manages coordination (e.g., authentication), but data is transferred directly between peers.

- **Example:** Video conferencing apps, where a server initiates the call, but video/audio streams directly between participants.

- **Advantages:**
    - **Efficiency:** Reduces server workload by allowing direct peer data sharing.
    - **Control:** A central server can still manage user authentication and session control.

- **Disadvantages:**
	- **Complex Implementation:** Requires sophisticated design.
	- **Potential Single Point of Failure:** If the coordinating server fails, peer discovery may be disrupted.

![[Pasted image 20250617115556.png]]


## Cloud Architecture

- **Definition:** Computing infrastructure hosted and managed by third-party providers (e.g., AWS, Google Cloud), operating on a virtualized client-server model.

- **Example:** Google Drive or Dropbox (Software as a Service - SaaS).

- **Key Characteristics:** On-demand self-service, broad network access, resource pooling, rapid elasticity, and measured service.

- **Advantages:**
    - **Scalability:** Easily adjust resources based on demand.
    - **Reduced Cost:** No need to manage physical hardware.
    - **Flexibility:** Access services from anywhere with an internet connection.

- **Disadvantages:**
	- **Vendor Lock-in:** Difficult to migrate between cloud providers.
	- **Security/Compliance:** Relies on a third party for data security.
	- **Connectivity Dependent:** Requires a stable internet connection.


## Software-Defined Architecture (SDN)

- **Definition:** Separates the network's *control plane* (decision-making) from the *data plane* (traffic forwarding). A *centralized software controller* manages network traffic.

- **Example:** Large data centers use SDN to *manage traffic flow* and *allocate bandwidth* dynamically. The control plane decide which flow needs more bandwidth based on the situation.

- **Advantages:**
	- **Centralized Control:** Simplifies overall network management.
	- **Programmability:** Network policies can be automated and changed quickly.
	- **Efficiency:** Optimizes traffic flows and resource use.

- **Disadvantages:**
	- **Controller Vulnerability:** The central controller is a single point of failure.
	- **Complex Implementation:** Requires specialized skills and tools

![[Pasted image 20250617122917.png]]


| `Architecture`  | `Centralized`                   | `Scalability`        | `Ease of Management`               | `Typical Use Cases`                |
| --------------- | ------------------------------- | -------------------- | ---------------------------------- | ---------------------------------- |
| `P2P`           | Decentralized (or partial)      | High (as peers grow) | Complex (no central control)       | File-sharing, blockchain           |
| `Client-Server` | Centralized                     | Moderate             | Easier (server-based)              | Websites, email services           |
| `Hybrid`        | Partially central               | Higher than C-S      | More complex management            | Messaging apps, video conferencing |
| `Cloud`         | Centralized in provider’s infra | High                 | Easier (outsourced)                | Cloud storage, SaaS, PaaS          |
| `SDN`           | Centralized control plane       | High (policy-driven) | Moderate (needs specialized tools) | Datacenters, large enterprises     |
## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3242)