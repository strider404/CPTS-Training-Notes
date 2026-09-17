
2025-06-19 10:20

Tags: #network  

## Network Security

- **CIA Triads**:
	- *Confidentiality*: Ensures only *authorized users* can view data.
	- *Integrity*: Guarantees that data is *accurate* and has not been altered.
	- *Availability*: Makes certain that network resources are *accessible* when needed.


## Firewalls

- **Definition:** A *security device* (hardware, software, or both) that monitors and *filters* incoming and outgoing network traffic based on a *set of security rules*.

- **Function:** It acts as a *barrier* between a trusted internal network and an untrusted external network (like the internet), *allowing* or *blocking* traffic based on factors like IP addresses, port numbers, and protocols.

- **Types of Firewalls**:
	- **Packet Filtering:** A basic type that operates at the *Network* and *Transport* layers (Layers 3 & 4) of the OSI model, examining *packet headers* (source/destination IP, source/destination port, and protocol type)
	- **Stateful Inspection:** *Tracks the state of active network connections*, making more intelligent filtering decisions than simple packet filtering.
	- **Application Layer (Proxy):** Operates at the *Application layer* (Layer 7), allowing it to *inspect the content of the traffic* itself (e.g., HTTP requests).
	- **Next-Generation Firewall (NGFW):** An advanced firewall that integrates traditional *stateful inspection* with *modern security features* like deep packet inspection (DPI), intrusion prevention (IPS), and application control.

- **Placement:** In *home* networks, firewalls are often built into the *router*. In larger *business* networks, they are typically *dedicated hardware devices* placed between the router and the internal network.

![[Pasted image 20250619103526.png]]


## Intrusion Detection and Prevention Systems (IDS/IPS)

- **Definition:** Security systems that monitor network or system activities for malicious actions or policy violations.

- **Key Distinction:**
    - **IDS (Intrusion Detection System):** Detects a potential threat and *generates an alert*. It is a *passive* monitoring system.
    - **IPS (Intrusion Prevention System):** Detects a potential threat and *actively takes steps* to block or prevent it. It is an *active*, inline system.

- **Detection Methods:**
	- **Signature-based:** Compares network traffic against a database of *known* attack patterns (signatures).
	- **Anomaly-based:** Establishes a *baseline* of normal network behavior and flags any significant deviations as suspicious.

- **Types of IDS/IPS:**
	- **Network-Based (NIDS/NIPS):** Deployed at *strategic points within the network* to monitor traffic flowing across that segment.
	- **Host-Based (HIDS/HIPS):** Installed on *individual devices* (like servers or workstations) to monitor their specific activity.

- **Placement:** Commonly placed behind a firewall to inspect already-filtered traffic, within a DMZ to protect public-facing servers, or directly on endpoint devices.

![[Pasted image 20250619110838.png]]



## References:

[Network Foundations](https://academy.hackthebox.com/module/289/section/3244)