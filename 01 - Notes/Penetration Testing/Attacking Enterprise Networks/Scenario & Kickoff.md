
2026-06-03 16:07

Tags: 

## Scenario & Kickoff

- **Client:** Inlanefreight (contracting Acme Security, Ltd.).
    
- **Objective:** Perform a full-scope External Penetration Test to identify perimeter vulnerabilities and simulate what an anonymous internet attacker can achieve.
    
- **Ultimate Goal:** If the DMZ is breached, pivot into the internal network and attempt full Active Directory domain compromise.
    
- **Testing Style:** Black-box (no credentials provided for web applications, VPN, or AD) and non-evasive (focus on finding as many vulnerabilities as possible).

## Rules of Engagement (RoE) & Scope

- **In-Scope External:**
    - `10.129.x.x` (external-facing target host)
        
    - `*.inlanefreight.local` (all subdomains requiring discovery)


- **In-Scope Internal:**
    - `172.16.8.0/23`
        
    - `172.16.9.0/23`
        
    - `INLANEFREIGHT.LOCAL` (Active Directory domain)


- **Permitted Activities:** Automated enumeration, vulnerability scanning, and network discovery (must avoid service disruption).


- **Strictly Out of Scope:**
    - Phishing and Social Engineering against employees or customers.
        
    - Physical security attacks against facilities.
        
    - Denial of Service (DoS) or any destructive actions.
        
    - Environment modifications without written authorization.


![[Pasted image 20260603160941.png]]
## References:

