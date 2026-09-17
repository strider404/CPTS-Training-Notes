
2026-05-21 11:24

Tags: #escalation  

## SeTakeOwnershipPrivilege

- **Function:** Grants the ability to *take ownership of any "securable object*" (files, folders, AD objects, registry keys, services, processes) by assigning `WRITE_OWNER` rights.
	- ![[Pasted image 20260521112733.png]]


- **Typical Users:** Assigned to Administrators by default, but occasionally granted to service accounts handling backups or VSS snapshots.


- **Attack Vector:** Allows an attacker to *seize control of sensitive files or folders* where access is normally denied, leading to data exfiltration, Remote Code Execution (RCE), or Denial-of-Service (DoS).


- **Group Policy Path:** `Computer Configuration > Windows Settings > Security Settings > Local Policies > User Rights Assignment`.
	- ![[Pasted image 20260521112721.png]]

## Exploitation Methodology

- **1.Verify and Enable Privilege:**
	- Check current status using `whoami /priv`.
	- ![[Pasted image 20260521113406.png]]
	    
	- If listed as `Disabled`, run a custom PowerShell script (e.g., `EnableAllTokenPrivs.ps1`) to activate it for your current session.
	- ![[Pasted image 20260521112840.png]]


- **2.Identify Target File:**
	- Locate a restricted file (e.g., `C:\Department Shares\Private\IT\cred.txt`).
	    
	- Use `Get-ChildItem` or `dir /q` to check current ownership and permissions (this may initially return empty or access denied).
		- ![[Pasted image 20260521113019.png]]
		- ![[Pasted image 20260521113106.png]]

- **3.Seize Ownership:**
	- Execute `takeown /f <target_file_path>`.
		- ![[Pasted image 20260521113115.png]]
		    
	- Verify the change using `Get-ChildItem` piped to `Select-Object` to confirm your user is now the owner.
		- ![[Pasted image 20260521113124.png]]

- **4.Modify Access Control Lists (ACL):**
	- As the new owner, you now have the right to change the object's permissions.
	    
	- Execute `icacls <target_file_path> /grant <your_username>:F` to grant your user Full Control over the file.
	- ![[Pasted image 20260521113204.png]]


- **5.Access the Data:**
	- Read the file locally using `cat` (PowerShell) or `type` (CMD).
	    
	- Exfiltrate the file back to your attack system for offline analysis (like cracking).


## High-Value Targets

- **System Files:** `%WINDIR%\repair\sam`, `%WINDIR%\repair\system`, and `.sav` registry backups.
    
- **Web Configurations:** `c:\inetpub\wwwwroot\web.config`.
    
- **Event Logs:** `%WINDIR%\system32\config\SecEvent.Evt`.
    
- **User Data:** KeePass databases (`.kdbx`), OneNote notebooks, SSH keys, or plaintext files containing passwords (`creds.txt`, `pass.*`).


## References:

