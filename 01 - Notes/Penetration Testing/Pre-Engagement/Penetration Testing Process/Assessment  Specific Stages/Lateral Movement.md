
2025-08-07 08:56

Tags:  

## Lateral Movement

- **Lateral Movement** is the phase that occurs after successfully gaining initial access (Exploitation) and *escalating privileges* on a single machine (Post-Exploitation).

- The primary objective is to determine **how far** an attacker can move _within_ the internal corporate network from the initial point of entry.

## The Process

- **Pivoting:** Using the initially compromised host as a proxy or "*pivot point*" to scan and attack internal network segments that are not publicly accessible. This is also known as tunneling.

- **Evasive Testing:** Actively attempting to *bypass* internal security controls like network segmentation, Intrusion Prevention/Detection Systems (IPS/IDS), and Endpoint Detection and Response (EDR) to avoid alerting defenders (the blue team).

- **Information Gathering:** Performing *reconnaissance* from the _inside_ of the network to discover other hosts, servers, and services that can now be reached.

- **Vulnerability Assessment:** *Analyzing* systems from an internal perspective, focusing on *misconfigurations*, weak user permissions, and insecure information sharing practices that are more common internally.

- **(Privilege) Exploitation:** Using the discovered internal vulnerabilities to *gain access* to other systems. This often involves reusing credentials or employing techniques like "pass-the-hash" attacks.

- **Post-Exploitation:** Once a new internal system is compromised, this phase is repeated to collect local system information and business data as evidence of expanded access.
## References:

https://academy.hackthebox.com/module/90/section/942