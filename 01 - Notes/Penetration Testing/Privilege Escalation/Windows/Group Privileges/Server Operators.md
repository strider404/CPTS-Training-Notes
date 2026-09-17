
2026-05-22 15:21

Tags: #escalation 

## Server Operators

- **Group Privileges:** The Server Operators group is a highly privileged built-in group. Members can log into Windows servers and Domain Controllers locally, control local services, and inherently possess **SeBackupPrivilege** and **SeRestorePrivilege**.


- **Service Enumeration:**
    - Use *sc.exe qc* (e.g., AppReadiness) to confirm a service runs with LocalSystem privileges.
        - ![[Pasted image 20260522152310.png]]
            
    - Use Sysinternals' *PsService.exe* security to verify that the Server Operators group has **SERVICE_ALL_ACCESS** (full control) over the target service.
        - ![[Pasted image 20260522152917.png]]


## Exploitation Steps

- **Verify current access:** Check the local Administrators group (net localgroup Administrators) to ensure your target account is not already a member.
	- ![[Pasted image 20260522153018.png]]


- **Modify the service:** Change the service's binPath to execute a command that adds your user to the local Administrators group: `sc config AppReadiness binPath= "cmd /c net localgroup Administrators /add"`.
	- ![[Pasted image 20260522153029.png]]


- **Trigger execution:** Attempt to start the modified service with `sc start` . The start request will fail and throw Error 1053 (which is expected), but the injected payload will still successfully execute as SYSTEM.
	- ![[Pasted image 20260522153357.png]]

## Post-Exploitation

- **Verify privilege escalation:** Run `net localgroup Administrators` again to confirm your user was successfully added.
	- ![[Pasted image 20260522153444.png]]


- **Domain Controller takeover:** With local admin rights on the DC, you have full control over the domain.


- **Extract credentials:** Tools like crackmapexec can be used to confirm administrative access (Pwn3d!), and secretsdump.py can be used to extract all NTLM password hashes (including the Domain Administrator's) directly from the NTDS database.
	- ![[Pasted image 20260522153506.png]]
## References:
https://academy.hackthebox.com/app/module/67/section/606
