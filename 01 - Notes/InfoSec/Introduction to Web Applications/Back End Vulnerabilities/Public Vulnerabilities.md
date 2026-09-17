
2025-07-25 12:05

Tags: #web  

## Public Vulnerabilities

- **Origin:** Critical back-end vulnerabilities often stem from *coding errors* and can be exploited remotely without local server access.

- **CVE System:** Discovered vulnerabilities are typically *patched* and then assigned a **Common Vulnerabilities and Exposures (CVE)** record, which includes a *severity score.*

- **Exploitation Process:** The initial step for a penetration tester is to identify the target application's **version**. With this information, one can search for public exploits in databases like **Exploit DB** and **Rapid7 DB**.

- **Prioritization:** The focus is generally on exploits that lead to **Remote Code Execution (RCE)** or have a high **CVSS score** (8-10).


## Common Vulnerability Scoring System (CVSS)

- **Definition:** CVSS is an open industry standard used to assess and score the severity of security vulnerabilities.

- **Purpose:** It provides a consistent scoring method to help organizations prioritize threat responses.

- **Metrics:** A CVSS score is calculated from three metric groups:
	- **Base:** Represents the inherent qualities of a vulnerability. The [National Vulnerability Database (NVD)](https://nvd.nist.gov/vuln-metrics/cvss) provides these scores.
	  
	- **Temporal:** Reflects characteristics that change over time, such as the availability of an exploit.
	  
	- **Environmental:** Accounts for factors specific to an organization's environment.

- **Versions:** The two primary versions are **CVSS v2** and **CVSS v3**. They differ in their metrics and severity rating scales, with v3 introducing a "Critical" category for scores from 9.0 to 10.0.

## Back-end Component Vulnerabilities

- **Web Servers:** Vulnerabilities in publicly accessible web servers (e.g., Apache, Nginx) are highly critical. A well-known example is **Shell-Shock**.

- **Internal Systems:** Vulnerabilities in the back-end operating system or database are typically exploited _after_ an attacker has already gained initial access to the network or server.

- **Goal:** These internal exploits are often used for **privilege escalation** or to move laterally to other systems within the network.

- **Mitigation:** Although not always directly exploitable from the internet, patching these internal vulnerabilities is crucial to prevent a full system compromise.
## References:

https://academy.hackthebox.com/module/75/section/763