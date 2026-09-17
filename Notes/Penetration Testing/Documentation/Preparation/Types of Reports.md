
2026-05-30 11:12

Tags: #documentation 

## Types of Reports

| **Assessment Type**          | **Core Focus**                                                                                                                                  | **Exploitation?** | **Key Deliverable**                                                                         |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------- |
| **Vulnerability Assessment** | Automated scanning (internal or external). Focuses on identifying and validating flaws to weed out false positives.                             | No                | A report highlighting vulnerability patterns, severity levels, and procedural deficiencies. |
| **Penetration Testing**      | Goes beyond scanning to actively exploit vulnerabilities. Aims to gain footholds, escalate privileges, and move laterally (often targeting AD). | Yes               | A detailed narrative of attack chains, compromised hosts, and validated business impact.    |
## Testing Perspectives and Methodologies

- Penetration tests can be adjusted based on the information provided and the level of stealth required by the client:

- **Knowledge Levels:**
    - **Black Box:** Zero prior knowledge (e.g., only given the company name or a raw network connection).
        
    - **Grey Box:** Partial knowledge (e.g., in-scope IP addresses or CIDR ranges).
        
    - **White Box:** Full knowledge (e.g., provided with credentials, source code, and configurations).


- **Evasion Levels:**
    - **Non-Evasive:** "Noisy" testing to find as many vulnerabilities as quickly as possible.
        
    - **Hybrid Evasive:** Starts stealthy to test Blue Team detection, then switches to non-evasive once caught. Great for testing mature defenses.
        
    - **Adversary Simulation / Red Teaming:** Long-term, highly stealthy engagements meant to simulate advanced persistent threats (APTs).

## Inter-Disciplinary Assessments

- Some engagements require highly specialized skills or collaboration across different domains:

- **Purple Teaming:** A collaborative effort where the penetration tester (Red) works directly with the incident responder/internal security (Blue) to tune alerting and detection tools.
    
- **Cloud, IoT, and Hardware Testing:** Specialized tests requiring deep knowledge of non-traditional infrastructure (serverless apps, hardware desoldering, container breakouts). _Note: Destructive hardware testing requires strict Rules of Engagement (RoE)._
    
- **Web Application Testing:** Can blend app-level exploitation with network-level pivoting to see how far an attacker can go after breaching a web portal.

## The Reporting Lifecycle

- Reporting is rarely a "one-and-done" process. It is a collaborative lifecycle that ensures the client gets actionable value.

- **1. The Draft Report**
	- You should almost always submit a draft first. This allows the client to review the findings, add management responses, clarify technical details, and suggest tonal adjustments before finalizing.

- **2. The Final Report**
	- Once the client approves the draft, the final report is issued. This is the official document often required by third-party auditing firms to fulfill compliance obligations.

- **3. Post-Remediation (Retest) Report**
	- Clients frequently ask you to retest their network after they have applied patches (especially for PCI compliance).
	  
	- **Crucial Rule:** Only test the _original findings_ on the _originally affected hosts_. Do not run new broad scans or fall into scope creep. Ensure retesting happens within a reasonable timeframe so you are comparing "apples to apples."

- **4. Attestation Letter**
	- A high-level, 1-to-2-page document confirming a penetration test took place. It contains zero sensitive data (no credentials or specific exploits) and is designed for the client to hand to their third-party vendors or partners as proof of security hygiene.

## Supplemental Deliverables

- **Slide Decks:** Tailored presentations. _Executive decks_ should focus on high-level risk and relatable industry anecdotes, while _Technical decks_ focus on the attack paths.
    
- **Spreadsheet of Findings:** A tabular, CSV/Excel export of your findings. This is highly valuable for clients who need to import the data into internal ticketing systems (like Jira) or prioritize remediation using pivot tables.
    
- **Vulnerability Notifications:** Out-of-band, emergency alerts issued _during_ the assessment. If you find a critical, internet-facing exploit (like unauthenticated RCE), you must stop and notify the client immediately so they can patch it before the engagement ends. Keep these brief, technical, and actionable.
## References:

https://academy.hackthebox.com/app/module/162/section/1538