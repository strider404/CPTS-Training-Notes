
2025-09-03 09:51

Tags: #footprint  

## Enumeration Methodology

- A standardized, yet flexible, **six-layer enumeration methodology** designed for both external and internal penetration tests.

![[Pasted image 20250903095208.png]]


- **Layer 1: Internet Presence:** Identify all **externally accessible infrastructure** and potential targets, including domains, subdomains, IP netblocks, and cloud instances.


- **Layer 2: Gateway:** Analyze the protective **security measures** defending the infrastructure, such as firewalls, Intrusion Prevention/Detection Systems (IPS/IDS), proxies, and network segmentation.


- **Layer 3: Accessible Services:** Examine **all services running on target systems** to understand their purpose, version, configuration, and functionality.


- **Layer 4: Processes:** Understand the **internal processes**, data flows, and dependencies associated with the accessible services.


- **Layer 5: Privileges:** Identify the **user accounts, groups, permissions**, and restrictions tied to the services to discover potential misconfigurations or escalation paths.


- **Layer 6: OS Setup:** Once internal access is achieved, **gather information** on the operating system's configuration, patch level, and sensitive files to assess the internal security posture.

## References:

https://academy.hackthebox.com/module/112/section/1185