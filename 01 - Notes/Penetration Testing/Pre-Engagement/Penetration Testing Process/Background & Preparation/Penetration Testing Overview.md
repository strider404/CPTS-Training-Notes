
2025-08-06 11:08

Tags:  

## Penetration Testing Fundamentals

- **Purpose**: A Penetration Test (Pentest) is an **authorized, simulated attack** on an organization's IT infrastructure to *identify and assess security vulnerabilities*.
  
- **Goal**: The primary objective is to uncover **all possible vulnerabilities** and evaluate their potential impact on the confidentiality, integrity, and availability (CIA) of systems and data.
  
- **Distinction from Red Teaming**: Unlike a pentest, a red team assessment is often *scenario-based*, focusing only on the vulnerabilities needed to achieve a specific, narrow objective (e.g., accessing a particular mailbox).

## Role in Risk Management

- **Function**: Pentesting is a critical part of a company's overall **IT security risk management** process.

- **Risk Handling**: Organizations cannot eliminate all risks. They can manage them by:
	- **Accepting** the risk.
	  
	- **Transferring** it (e.g., through insurance or contracts).
	  
	- **Avoiding** it.
	  
	- **Mitigating** it through security controls.


- **Pentester's Responsibility**: The tester's role is to act as a trusted advisor by **reporting findings**, providing detailed reproduction steps, and recommending remediation. They **do not** implement the fixes themselves.

- **Scope**: A pentest provides a **"momentary snapshot"** of security at a single point in time, not continuous monitoring.


## Vulnerability Assessments vs. Penetration Tests

- **Vulnerability Assessment**:
	- Relies almost exclusively on **automated scanning tools** (e.g., Nessus, OpenVAS).
    
	- Checks for known vulnerabilities without adapting to the specific target configuration.

- **Penetration Test**:
	- Combines **automated tools with extensive manual testing** and validation.
	  
	- Is tailored specifically to the system being tested.

- **Authorization**: Explicit, **written authorization is mandatory** for any testing, as the activities could otherwise be considered criminal offenses. This may also require permission from third-party hosting providers.


## Testing Methodologies

- **Perspectives**
	- **External Pentest**: Simulates an attack from the *public internet* to test the external network perimeter. The goal is to breach defenses and gain internal access.
    
	- **Internal Pentest**: Simulates an attack from *within the corporate network*, often assuming a breach has already occurred or a malicious insider is present.

- **Information Levels**
	- **Blackbox**: The tester receives almost no information about the target. This requires significant time for reconnaissance.
	  
	- **Greybox**: The tester is given partial information, such as user credentials or specific hostnames.
	  
	- **Whitebox**: The tester receives full information, including source code, admin credentials, and network diagrams, allowing for the most comprehensive assessment.
	  
	- **Red-Teaming**: Can be combined with other types and may include physical security tests and social engineering.
	  
	- **Purple-Teaming**: A collaborative exercise where attackers (Red Team) and defenders (Blue Team) work together to improve security in real-time.


- The **scope** of a pentest can include a wide variety of assets, such as:
    - Networks and Servers
      
    - Web, Mobile, and API applications
      
    - Cloud Infrastructure
      
    - Physical Security
      
    - Employees (via social engineering)

## References:

https://academy.hackthebox.com/module/90/section/935