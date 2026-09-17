
2026-05-22 18:21

Tags: #escalation 

## User Account Control

- **Purpose:** User Account Control (UAC) is a *convenience feature* (not a strict security boundary) that **prevents unintended system changes by requiring a consent prompt for elevated activities.**


- **Integrity Levels:** Applications run under specific *integrity levels*. By default, processes launched by an administrator run at a medium mandatory level (standard user context) unless explicitly elevated.


- **Admin Approval Mode (AAM):** The default built-in Administrator (RID 500) always operates at *high integrity*. Other administrative accounts operate at *medium integrity* and are assigned two separate access tokens upon login (unprivileged and privileged).

## UAC Enumeration

- **Check User Context:** Use `whoami /user` and `whoami /priv` to view current group memberships and active privileges.


- **Verify UAC is Enabled:** Query the registry key `HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA` (Value `0x1` means enabled).
	- ![[Screenshot_20260522_182606.png]]


- **Determine UAC Level:** Query `ConsentPromptBehaviorAdmin` in the registry. A value of `0x5` indicates "Always notify" (the highest level with the fewest bypasses).
	- ![[Screenshot_20260522_182625 1.png]]


- **Identify Windows Build:** Use PowerShell (`[environment]::OSVersion.Version`) to get the build number (e.g., 14393 translates to release 1607). This is required to [cross-reference](https://en.wikipedia.org/wiki/Windows_10_version_history) applicable bypasses on repositories like the **UACME** project.
	- ![[Screenshot_20260522_182647.png]]
	- ![[Pasted image 20260522182737.png]]

## UAC Bypass via DLL Hijacking (UACME Technique 54)

- **The Vulnerability:** Windows auto-elevates certain trusted binaries without a prompt. The 32-bit auto-elevating binary `SystemPropertiesAdvanced.exe` attempts to load a non-existent DLL (`srrstr.dll`).


- **The Execution Path:** If the DLL isn't found in system folders, Windows searches the directories listed in the `%PATH%` environment variable.


- **Exploitation Steps:**
    1. **Enumerate PATH:** Run `cmd /c echo %PATH%` to find a user-writable directory. (e.g., `C:\Users\<user>\AppData\Local\Microsoft\WindowsApps`).
        
    2. **Generate Payload:** Create a malicious DLL reverse shell using `msfvenom` (`-f dll > srrstr.dll`).
        1. ![[Screenshot_20260522_182932.png]]
            
    3. **Plant the Payload:** Transfer the malicious `srrstr.dll` into the writable folder discovered in the `%PATH%`.
        
    4. **Clean Up:** Kill any lingering `rundll32.exe` processes (`taskkill /PID <PID> /F`) to avoid execution conflicts.
        
    5. **Trigger Execution:** Execute the vulnerable 32-bit binary from the command line: `C:\Windows\SysWOW64\SystemPropertiesAdvanced.exe`.


- **Result:** The trusted binary auto-elevates to high integrity, searches the `%PATH%`, finds the malicious `srrstr.dll`, and executes it, granting an elevated reverse shell with all administrative privileges unlocked.

## References:

