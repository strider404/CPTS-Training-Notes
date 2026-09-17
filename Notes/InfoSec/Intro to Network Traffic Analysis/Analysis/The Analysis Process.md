
2025-06-25 11:23

Tags: #network  

## The Analysis Process

- **Definition:** NTA is the detailed examination of network data to determine the origin and impact of events.

- **Primary Goal:** To identify deviations from normal network activity, which could indicate malicious actions (e.g., unauthorized remote access), or operational issues.

- **Key Benefit:** NTA provides critical **visibility** into network communications, which is essential for both security and operational management.

#### The NTA Process and Its Value

- **Establishing a Baseline:** A crucial step is to capture and analyze traffic over time to *create a baseline of what is considered "normal"* for the network. This makes anomaly detection significantly more efficient.

- **Security & Defense:**
	- It allows defenders to detect and respond to security incidents more quickly.
	- NTA is invaluable when integrated with other security tools like Intrusion Detection/Prevention Systems (IDS/IPS), firewalls, and Security Information and Event Management (SIEM) systems such as Splunk or the ELK Stack.

- **Network Operations:** It facilitates *troubleshooting of connectivity problems* and helps verify that infrastructure and protocols are functioning correctly.

- **Human Analyst Role:**
	- While automated tools are useful, they should not be the sole source of analysis.
	- Malicious actors continuously evolve techniques to bypass automated defenses, making manual verification by a human analyst an indispensable part of the process.

## Analysis Dependencies

- NTA can be performed using *two primary methods* for capturing traffic, each with its own set of requirements

- **Passive Analysis**:
	- **Description:** This method involves *copying traffic data without interacting with the original packets*. It is *less intrusive* than active analysis.
	- Dependencies:
		- **Permission:** Written authorization is mandatory to avoid legal and policy violations.
        
        - **Mirrored Port (SPAN Port):** A *switch or router interface* must be configured to duplicate traffic from other ports or VLANs to your analysis machine.
        
        - **Capture Tool:** Software such as *Wireshark* or *TCPDump* is needed to ingest the traffic.
        
        - **Storage and Processing Power:** Required to handle potentially *large PCAP files*.


- **Active (In-line) Analysis:**
	- **Description:** This is a hands-on approach where a *capture device is placed directly in the path of the network traffic.*
	- Dependencies:
		- **Permission:** As with passive analysis, this is a strict requirement.
    
		- **In-line Placement:** Requires a *change to the network's physical or logical topology.*
    
		- **Network TAP or Multi-NIC Host:** A *physical TAP (Test Access Point) device* or a computer with at least two Network Interface Cards (NICs) is necessary to intercept traffic while allowing it to flow to its destination.
    
		- **Capture Tool:** Software to ingest the data.
    
		- **Significant Storage and Processing Power:** This method often captures a *much larger volume of traffic* (e.g., from a layer three link), demanding substantial system resources.

## References:

[Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/81/section/953)