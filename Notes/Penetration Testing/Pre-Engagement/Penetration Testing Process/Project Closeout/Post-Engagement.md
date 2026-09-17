
2025-08-07 11:01

Tags:  

## Post-Engagement

- This phase occurs **after** testing is complete.
  
- It involves **deleting tools/scripts** and reverting any configuration changes made on the target systems.

- All activities, including cleanup actions, must be meticulously **documented**.

- If any cleanup **cannot** be performed, the client **must be notified**, and the issue must be documented in the report appendices.

- All changes, even those successfully reverted, should be documented in the report for the client's records.

## Documentation and Reporting

- Adequate documentation for all findings (e.g., command output, screenshots) must be collected before disconnecting from the client's network.

- All scan data, logs, and other relevant information must be retrieved.

- Sensitive data, such as Personally Identifiable Information (PII), should not be retained.

- A draft report is created as the first deliverable for the client. The report should include:
    - An attack chain detailing the steps of a compromise.
      
    - An executive summary for a non-technical audience.
      
    - Detailed findings with risk ratings, impact, and remediation recommendations.
      
    - Reproducible steps for each finding.
      
    - Near, medium, and long-term recommendations.
      
    - Appendices containing scope, OSINT data, compromised assets, system modifications, and other supplementary data.

## Report Review Meeting

- After the client reviews the draft report, a meeting is held.

- The purpose is to walk through the findings, provide explanations, and answer client questions.

- The meeting is not a word-for-word reading of the report but focuses on key findings and client queries.


## Deliverable Acceptance

- The process for accepting deliverables should be defined in the Scope of Work (SOW).

- The client provides feedback on the draft report.

- After incorporating feedback, a `FINAL` version of the report is issued.

## Post-Remediation Testing

- This is often included in the project's cost.

- The tester re-accesses the environment to verify that the client has successfully remediated the reported vulnerabilities.

- A post-remediation report is issued, showing the status of each finding (e.g., "Remediated," "Not Remediated") with evidence.

![[Pasted image 20250807111804.png]]

## Role of the Pentester in Remediation

- Penetration testers must remain impartial third-party auditors.

- They should not perform remediation tasks (e.g., fixing code, patching systems).

- Their role is to act as a trusted advisor, providing general remediation advice and clarification, not specific implementation details. This maintains the integrity of the assessment and avoids conflicts of interest.

## Data Retention

- Policies for retaining and destroying client data must be defined in the contract.

- It is best practice to retain evidence for a period to answer future questions or assist with retesting.

- Any retained data must be stored securely and encrypted at rest.

- All engagement data should be wiped from the tester's local systems after the assessment concludes.

## Close Out

- The project is closed after the final report is delivered, post-remediation testing is complete, and client questions are resolved.

- Final steps include ensuring all client data is securely wiped or stored according to policy, invoicing the client, and collecting payment.

- A post-assessment client satisfaction survey is recommended for continuous improvement.
  
- Professionalism, communication, and client interactions are emphasized as being just as important as technical skills for future work.
## References:

https://academy.hackthebox.com/module/90/section/944