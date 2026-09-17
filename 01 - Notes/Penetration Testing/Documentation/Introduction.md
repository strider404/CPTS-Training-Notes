
2026-05-30 10:17

Tags: #documentation

## Introduction

- A critical concept for any report is establishing that a penetration test only reflects the network's security status during a specific window of time.

- Your report's overview should always include:
	- **Logistics:** The type of work, who performed it, and special considerations (e.g., remote over VPN vs. onsite).
	    
	- **Source Data:** The source IP addresses used during the test.
	    
	- **Timeframe & Disclaimer:** Explicit start and end dates, alongside a disclaimer stating that the report does not cover any changes or vulnerabilities introduced outside of this testing window.

## Real-World Scenarios: Documentation in Practice

|**Scenario**|**The Crisis**|**How Documentation Saved the Day**|**Lesson Learned**|
|---|---|---|---|
|**Exploding VM**|A testing VM completely crashed during a month-long external test.|Daily evidence backups to a shared drive allowed the tester to restore a fresh VM and lose zero work.|Always follow a strict, daily backup process for your testing evidence.|
|**Ping of Death**|A hostile client accused the tester of taking down critical servers during an internal test.|Timestamped logs, raw scan data, and confirmed scope files proved the tester only targeted approved IPs using safe methods.|Always ask clients for an explicit "Exclude/Do Not Scan" list beforehand.|
|**Slow as Molasses**|A network admin blamed the tester's scans for slowing the client's network to a halt.|Scan output proved best practices were used. The real issue was debug mode being mistakenly left on by the client's IT team.|Keep detailed logs to justify your actions and help clients accurately troubleshoot network issues.|


## References:

