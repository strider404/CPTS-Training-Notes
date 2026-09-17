
2025-04-25 16:29

Tags: #network  

## Networking Topologies (Cấu trúc mạng)

- **Network topology**: defines the *structure and arrangement*—physical or logical—of devices and connections in a network. Include:
	- **Host** (e.g., clients and servers)
	- **Network components** (e.g., switches, routers)
 
- **Physical topology** refers to the physical layout (cabling, node placement, connections).
    
- **Logical topology** describes how data flows across the network, regardless of physical setup.

## Network Topology Components:
- **Connections:**
	- _Wired:_ Coaxial, glass fiber, twisted-pair, etc.
	    
	- _Wireless:_ Wi-Fi, cellular, satellite, etc.

- **Nodes - Network Interface Controller (NICs):**
	- ==Devices== like NICs, repeaters, hubs, switches, routers, gateways, firewalls.
	    
	- Nodes can be ==computers== or ==simple devices== with limited or no programmability.

- **Classifications:**
	- Topologies can be _physical_ or _logical_ and do not have to match physical layouts.
	    
	- There are eight primary types:
	    - **Point-to-Point**, **Bus**, **Star**, **Ring**, **Mesh**, **Tree**, **Hybrid**, **Daisy Chain**
	        
	- Complex networks often use _hybrid topologies_, combining multiple types.

#### Point-to-Point

- A **direct, dedicated link** between two hosts.

- Simplest form of networking; ideal for mutual communication.

![[Pasted image 20250425163910.png]]

#### Bus

- All hosts share a **single transmission medium** (e.g., coaxial cable).

- No central component; **one host transmits**, ==others listen and determine if the data is for them==.

- Only **one host can send at a time** to avoid collisions.

- Simple but not scalable; performance degrades with more hosts.

![[Pasted image 20250425164032.png]]

#### Star

- All hosts connect to a **central device** (hub, switch, or router).

- Each device has a **separate link** to the central node.

- Central device manages traffic; **high load** at the center.

- ==Common in modern LANs== due to its scalability and fault isolation.

![[Pasted image 20250425164210.png]]


#### Ring

- Hosts are connected in a circular layout with **two cables** per host: one for **incoming**, one for **outgoing** data.

- No central device is needed; data flows in a **single, predefined direction**.

- Access is typically managed using a **token-passing** protocol to prevent collisions.

- A logical ring can be implemented on a physical star using a switch that emulates a ring.

![[Pasted image 20250425164705.png]]

#### Mesh

- Devices are **interconnected** either fully or partially.

- ==Used in WANs/MANs== for **high reliability and fault tolerance**.
	- Can't be used in LANs due to high cost (too many cables)

- In **fully meshed**, ==each host is connected to every other host.==
	- -> If 1 path is failed, we can go the other paths

- In **partially meshed**, the endpoints are connected by only one connection.

![[Pasted image 20250425170712.png]]

#### Tree

- A **hierarchical extension** of star topology, ideal for large networks.

- Common in enterprises and city-wide MANs.

- Can include both **logical (e.g., spanning tree)** and **physical structures**, often with a hub/switch hierarchy.

![[Pasted image 20250425170956.png]]

#### Hybrid

- Combines two or more topologies into one.
    
- A network is only considered hybrid if it integrates **distinct topology types** (e.g., bus + star).

- The image below is Star + Mesh

![[Pasted image 20250425171501.png]]


#### Daisy Chain

- Hosts are connected in **series**, forming a simple chain.

- Common in **automation systems** (e.g., CAN networks)

- Signals pass through each node ==in sequence==.

- Simple physical setup, but limited fault tolerance and scalability.

![[Pasted image 20250425171558.png]]

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/299)
