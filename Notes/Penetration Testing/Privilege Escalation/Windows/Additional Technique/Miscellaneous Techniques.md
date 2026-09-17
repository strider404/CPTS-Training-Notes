
2026-05-27 17:58

Tags: #escalation 

## Living Off The Land Binaries and Scripts (LOLBAS)

- The [**LOLBAS project**](https://lolbas-project.github.io/) catalogs native, Microsoft-signed files (binaries, scripts, libraries) that can be abused by attackers to evade detection. Because these tools are expected parts of the Windows operating system, they often bypass standard security controls.


- **Certutil:** Intended for handling certificates, but can be abused to download files from an attacker's server or to base64 encode/decode files on the target disk.
	- ![[Pasted image 20260527175914.png]]


- **Rundll32:** Can be utilized to execute malicious `.DLL` files (either hosted locally or over an SMB share) to obtain a reverse shell.

## Always Install Elevated

- This is a Local Group Policy misconfiguration where **Windows Installer is permitted to run with SYSTEM privileges** for any user.


- **Enumeration:** Checked via `reg query` on specific `HKEY_CURRENT_USER` and `HKEY_LOCAL_MACHINE` paths. If the `AlwaysInstallElevated` key is set to `0x1`, the system is vulnerable.
	- ![[Pasted image 20260527180013.png]]
	  
- **Exploitation:** An attacker can generate a malicious `.msi` file using **msfvenom** and execute it silently via the command line (`msiexec /i <file> /quiet /qn /norestart`) to trigger a reverse shell as `NT AUTHORITY\SYSTEM`.
	- ![[Pasted image 20260527180059.png]]

## CVE-2019-1388 (Windows Certificate Dialog Bypass)

- A flaw in the UAC mechanism allows a user to break out of the Windows Certificate Dialog and escalate privileges.


- **The Flaw:** When viewing the certificate of certain older, Microsoft-signed executables (like `hhupd.exe`), an OID field populated with a hyperlink can be clicked.


- **Exploitation:** Clicking the link launches a browser as `NT AUTHORITY\SYSTEM`. By right-clicking the webpage, selecting "View page source," and using the "Save as" dialog, an attacker can launch `cmd.exe` directly from the `System32` directory with full SYSTEM privileges.

## Insecure Scheduled Tasks

- **Scheduled tasks** running with *elevated privileges* can be hijacked if standard users are granted excessive permissions to the task's scripts or working directories.


- **Enumeration:** Tasks can be listed using the `schtasks` command or the `Get-ScheduledTask` PowerShell cmdlet.
	- ![[Pasted image 20260527180335.png]]
	- ![[Pasted image 20260527180327.png]]


- **Exploitation:** While standard users cannot view tasks created by administrators, they can hunt for improperly secured directories (e.g., `C:\Scripts` writeable by `BUILTIN\Users`). If an administrator has a scheduled task running a script from that directory, an attacker can *append malicious code* to the script to catch a SYSTEM-level beacon when the task runs.


## Information Gathering: Description Fields

- System administrators occasionally take shortcuts and store sensitive information, such as plain-text passwords, directly within system description fields.


- **User Descriptions:** Can be checked quickly using the `Get-LocalUser` cmdlet.
	- ![[Pasted image 20260527180425.png]]


- **Computer Descriptions:** Can be extracted using the `Get-WmiObject -Class Win32_OperatingSystem` cmdlet.
	- ![[Pasted image 20260527180439.png]]

## Mounting Virtual Disks (VHDX/VMDK)

- During enumeration (often aided by tools like **Snaffler**), you may find *backups of virtual hard drives* on network shares. These can be mounted locally to extract sensitive data from a live or backed-up machine.


- **Mounting:** Can be done in Linux using `guestmount` or in Windows using Disk Management and the `Mount-VHD` cmdlet.
	- ![[Pasted image 20260527180550.png]]


- **Exploitation:** Once mounted, you can navigate to `C:\Windows\System32\Config` and extract the **SAM**, **SECURITY**, and **SYSTEM** registry hives. Tools like **secretsdump.py** can then be used to dump local password hashes, potentially yielding a local administrator hash that works across the domain.
## References:

https://academy.hackthebox.com/app/module/67/section/635