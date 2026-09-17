
2026-05-23 09:00

Tags: #escalation 

## Permissive File System ACLs

- **Concept:** Service executables with *weak Access Control Lists (ACLs)* allow unprivileged users to modify or replace the file.


- **Identification:** Run `SharpUp.exe audit` to locate "Modifiable Service Binaries".
	- ![[Pasted image 20260523092622.png]]


- **Verification:** Use `icacls "C:\Path\To\Binary.exe"` to verify if groups like `Everyone` or `BUILTIN\Users` have Full `(F)` access.
	- ![[Pasted image 20260523092727.png]]


- **Exploitation:**
    1. Back up the legitimate binary.
       
    2. Replace the binary with a custom payload (e.g., generated via `msfvenom` to grant a reverse shell or add a local admin).
        
    3. Trigger execution via `sc start <ServiceName>`.
    4. ![[Pasted image 20260523092828.png]]


## Weak Service Permissions

- **Concept:** Services configured so that unprivileged users have *excessive control rights* over the service itself (e.g., `SERVICE_ALL_ACCESS`).


- **Identification:** Use `accesschk.exe /accepteula -quvcw <ServiceName>` to verify if your user or group has write/modify access.
	- ![[Pasted image 20260523093132.png]]


- **Exploitation:**
    1. Alter the service's execution path: `sc config <ServiceName> binpath="cmd /c net localgroup administrators <username> /add"`.
        1. ![[Pasted image 20260523093155.png]]
            
    2. Stop the service: `sc stop <ServiceName>`.
        
    3. Start the service: `sc start <ServiceName>`. (The service will throw an error since the binpath isn't a true service executable, but the malicious command will run).


- **Cleanup:** Revert the `binpath` back to the original executable path and restart the service to restore normal system operations.


## Unquoted Service Paths

- **Concept:** When a binary path contains spaces and lacks quotation marks, Windows breaks the path at each space and appends `.exe` while searching for the file (e.g., attempting `C:\Program.exe` before reaching `C:\Program Files\App\service.exe`).


- **Identification:** Execute `wmic service get name,displayname,pathname,startmode | findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """` to spot vulnerable paths.
	- ![[Pasted image 20260523093810.png]]


- **Exploitation:** Drop a malicious executable matching the broken path (like `Program.exe`) in an earlier directory sequence.


- **Caveat:** This is frequently found but rarely exploitable, as writing to root directories (like `C:\` or `C:\Program Files`) usually requires administrative privileges beforehand.

## Permissive Registry ACLs

- **Concept:** Weak permissions assigned to the Windows Registry keys that define and govern services.


- **Identification:** Use `accesschk.exe /accepteula "<username>" -kvuqsw hklm\System\CurrentControlSet\services` to find modifiable registry keys.
	- ![[Pasted image 20260523094525.png]]


- **Exploitation:** Utilize PowerShell's `Set-ItemProperty` to overwrite the `ImagePath` value with a malicious command or payload path.
	- ![[Pasted image 20260523094536.png]]

## Modifiable Registry Autorun Binaries

- **Concept:** Programs configured in the registry to run automatically upon system startup or user logon.


- **Identification:** Enumerate startup binaries using PowerShell: `Get-CimInstance Win32_StartupCommand | select Name, command, Location, User | fl`.
	- ![[Pasted image 20260523094612.png]]


- **Exploitation:** If you possess write access to the targeted registry key or the underlying executable, replace the binary with a payload. The escalation triggers the next time the target user logs in, executing the payload in their security context.
## References:

https://academy.hackthebox.com/app/module/67/section/628