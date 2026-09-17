
2026-05-21 10:49

Tags: #escalation  

## SeDebugPrivilege

- **Purpose:** Grants the ability to *debug programs, capture sensitive information* from system memory, and access or modify kernel and application structures.
	- ![[Pasted image 20260521105046.png]]


- **Target Audience:** By default, only given to administrators. However, it is frequently assigned to developers who need to debug system components.


- **Reconnaissance Strategy:** During an internal pentest, cross-reference captured hashes (e.g., from Responder) with OSINT (like LinkedIn) to prioritize cracking developer accounts, as they are likely to hold this privilege.


- **Verification:** Run `whoami /priv` from an elevated shell. The privilege can be exploited even if its state is listed as "Disabled".

## Attack Vector 1: Credential Dumping via LSASS

- **Objective:** Dump the memory of the Local Security Authority Subsystem Service (LSASS) process to extract logged-on users' NTLM hashes and cleartext passwords for Pass-the-Hash (PtH) attacks.


- **Execution Method A (Command Line):** Use the Sysinternals `procdump` tool.
    - _Command:_ `procdump.exe -accepteula -ma lsass.exe lsass.dmp`
    - ![[Pasted image 20260521105211.png]]


- **Execution Method B (GUI via RDP):** If you cannot load tools onto the target but have RDP access, you can manually dump memory.
    - _Steps:_ Open Task Manager -> Details tab -> right-click `lsass.exe` -> select **Create dump file**.
    - ![[Pasted image 20260521105304.png]]


- **Credential Extraction:** Transfer the `.dmp` file to your attack machine and parse it offline using **Mimikatz**.
    1. `log` (to save the output to a text file)
        
    2. `sekurlsa::minidump lsass.dmp` (to load the file)
        
    3. `sekurlsa::logonpasswords` (to extract the credentials)
    4. ![[Pasted image 20260521105237.png]]


## Attack Vector 2: Remote Code Execution (RCE) as SYSTEM

- **Objective:** Elevate privileges directly to `NT AUTHORITY\SYSTEM` by *altering standard system behavior* so a child process inherits the token of a highly privileged parent process.


- **Target Identification:** Identify a parent process running as SYSTEM (like `winlogon.exe` or `lsass.exe`) to hijack its token.
    - _Commands:_ Use `tasklist` or PowerShell's `Get-Process` to find the target's Process ID (PID).
    - ![[Pasted image 20260521105340.png]]


- **Exploitation:** Load a PowerShell PoC script (e.g., `psgetsystem`) to launch your payload.
    - _Syntax:_ `[MyProcess]::CreateProcessFromParent(<system_pid>,<command_to_execute>,"")`
        
    - _Note:_ The third blank argument `""` is strictly required for this specific PoC to function.
    - ![[Pasted image 20260521105440.png]]


- **Strategic Use Case:** This technique is critical when you lack RDP access, when dumping LSASS yields no useful credentials, or when you need to quickly upgrade a standard reverse shell or web shell directly to SYSTEM.
## References:

