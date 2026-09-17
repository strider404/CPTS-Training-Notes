
2025-08-06 14:47

Tags:  

## Open-Source Intelligence (OSINT)

- This involves gathering information from **publicly available sources** (e.g., code repositories like GitHub, social media, job postings).

- The objective is to **find sensitive data** such as passwords, API keys, SSH keys, and internal code that has been inadvertently exposed.

![[Pasted image 20250806145522.png]]

## Infrastructure Enumeration

- This activity aims to map the target's technical infrastructure, both on the internet and intranet.

- It employs a combination of OSINT and **active scanning techniques**, such as DNS queries, to identify servers, hosts, and their IP addresses.

- A key goal is to **identify security measures**, such as Web Application Firewalls (WAF), to plan for evasion tactics.

- From an internal perspective, this can help identify targets for attacks like password spraying.

## Service Enumeration

- This focuses on identifying the specific network services running on hosts and, critically, their **version numbers**.

- Knowing the service version is crucial for finding **known vulnerabilities** associated with outdated software.


## Host Enumeration

- This is a detailed **examination of individual hosts** specified in the scope of the test.

- The process aims to identify the operating system, all running services, service versions, open ports, and the host's function within the network.

- It highlights a common security flaw: **internal services are often less secure** due to an administrator's assumption that they are not accessible from the internet.

- This enumeration is also performed **post-exploitation** to find local files and information that can be used for privilege escalation.

## Pillaging

- This refers to the act of *collecting sensitive information locally* on a host _after_ it has been compromised (post-exploitation).

- The information gathered (e.g., user data, credentials) is used to demonstrate the impact of an attack and to facilitate privilege escalation or lateral movement within the network.


## References:

https://academy.hackthebox.com/module/90/section/938