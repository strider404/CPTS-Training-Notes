
2026-06-01 10:32

Tags: #documentation 

## Anatomy of a Finding

- A well-structured finding must contain enough information for technical teams to reproduce the issue and validate their subsequent fixes. Every finding should include these core components:
	- **Description:** An explanation of the vulnerability and the platforms it affects.
	    
	- **Impact:** The real-world consequences if the vulnerability remains unresolved.
	    
	- **Affected Scope:** Specific systems, networks, applications, or URLs.
	    
	- **Remediation:** Actionable steps to fix or mitigate the issue.
	    
	- **References:** Links to external documentation for further reading.
	    
	- **Reproduction Steps & Evidence:** A narrative walkthrough paired with proof of exploitation.
	    

- _Optional but recommended fields:_ CVEs, MITRE/OWASP IDs, CVSS scores, and the probability/ease of exploitation.

## Documenting Reproduction Steps and Evidence

- Assume the reader has technical knowledge but is _not_ a penetration tester. They may not know how your tools work or how to read raw terminal output.

- **Pacing and Narrative:** Break steps down logically. Use separate figures for setup (e.g., Metasploit module configuration) and execution. Write a clear narrative _between_ screenshots rather than cramming explanations into image captions.
    
- **Actionable Evidence:** Present evidence in a way the client can use. For instance, instead of a Burp Suite screenshot, provide the raw web request text so the client can copy/paste it to recreate the attack.
    
- **Defensible Proof:** Ensure your evidence leaves no room for debate. A screenshot of a basic auth login prompt doesn't prove credentials are sent in cleartext—a Wireshark packet capture does. Always include the target IP or URL in screenshots to prove the finding belongs to the client's environment.
    
- **Professionalism:** Redact sensitive information (passwords, hashes), disable unprofessional browser extensions, and hide your bookmarks bar before taking screenshots.
    
- **Alternative Tools:** Briefly mention and link to alternative validation tools (e.g., a Windows-friendly PowerShell script instead of a Linux binary) to make reproduction easier for the client's internal team.

## Crafting Effective Remediation Recommendations

|**Approach**|**Characteristics**|**Example**|
|---|---|---|
|**Poor Remediation**|Lazy, vague, or relies exclusively on expensive commercial tools.|_"Reconfigure your registry settings,"_ or _"Buy [Expensive Tool] to fix this."_|
|**Effective Remediation**|Specific paths/values, offers interim workarounds, and includes warnings about potential operational impacts.|_"Update registry hive [Path] to [Value]. Test this in a small group first to prevent outages. Alternatively, apply the vendor's interim workaround linked below."_|

## Selecting Quality References

- Provide external resources so the client can learn more about the root cause and the fix. Quality references should be:
	- **Vendor-Agnostic:** Avoid vendor blogs that prioritize selling a product over explaining the vulnerability.
	    
	- **Accessible & Concise:** Avoid paywalls, ad-heavy sites, or overly dense documentation (like massive RFCs) that take too long to parse.
	    
	- **Reputable:** Use stable, well-known sources that won't result in broken links a month later. Writing your own blog posts to use as references is highly encouraged.

## Tooling and Practice

- The lecture highlights [**WriteHat**](https://github.com/blacklanternsecurity/writehat), an open-source report writing tool developed by Black Lantern Security. Familiarizing yourself with reporting tools and practicing writing custom findings based on lab exercises is the best way to refine your documentation skills before engaging with real clients.
	- ![[Pasted image 20260601103649.png]]
## References:

