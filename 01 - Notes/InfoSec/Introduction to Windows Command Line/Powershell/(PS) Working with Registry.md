
2025-04-18 16:20

Tags: #windows #shell   

## (PS) Working with Registry

- [Latest section about Registry](<obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FWindows%20Fundamentals%2FWindows%20Security%20(2)>)

- **Windows Registry**: a ==hierarchical database== that stores ==configuration== settings and options for the operating system and installed applications

- Structure:
	- **Keys:** ==Act like folders==; they organize data hierarchically and can contain sub-keys and values. Naming is alphanumeric and not case-sensitive.
	- ![[Pasted image 20250418162816.png]]
	- **Values:** Hold ==actual data== associated with keys. Each value includes a name, type, and data.
	- ![[Pasted image 20250418162826.png]]

- **Registry Files**: all stored physically in **C:\Windows\System32\Config\**

- **Registry Hives**: set of predefined Registry keys (not actually stored as a folder in the machine)
	- **HKLM (HKEY_LOCAL_MACHINE):** System-wide hardware and software info (hardware and operating system data, bus types, memory, device drivers)
	  
	- **HKCC (HKEY_CURRENT_CONFIG):** Current hardware profile (shows the variance between current and default setups)
	  
	- **HKCR (HKEY_CLASSES_ROOT):** Filetype and UI settings.
	  
	- **HKCU (HKEY_CURRENT_USER):** Settings for the currently logged-in user.
	  
	- **HKU (HKEY_USERS):** The default User profile and current user configuration settings

- **Path to Registry** in Powershell: 
	- `Registry::<Hive>\...`: 
	- `HKLM:\...`: pre-mounted registry drive (just like C:/ or D:/)

- **PowerShell Cmdlets:**
	- `Get-Item`: Retrieves Registry ==keys==.
	- `Get-ItemProperty`: Retrieves key ==values== in a more readable format
		- e.g.,  `Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
	- `New-Item`: Create Registry key
		- `New-Item -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ -Name TestKey`
	- `New-ItemProperty`: Modifies or creates Registry values.
		- `New-ItemProperty -Path HKCU:\...\RunOnce\TestKey -Name "access" -Value "C:\Users\...\payload.exe"`
	- `Get-ChildItem`: Lists subkeys and can recursively search with `-Recurse`
	- `Remove-ItemProperty`: Delete Registry values

- **reg.exe**: shorter way to access Registry via PS
	- `reg query`: Registry searches
		- `/F`: search pattern (`"password"`)
		- `/t`: type filter (e.g., `REG_SZ`)
		- `/S`: recursive search
		- `/K`: restrict to key names only
		- e.g., `REG QUERY HKCU /F "password" /t REG_SZ /S /K`
	- `reg add`: create new Registry key & values
		- `/v`: value
		- `/t`: type
		- `/d`: directory
		- e.g., `reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\TestKey" /v access /t REG_SZ /d "C:\Users\htb-student\Downloads\payload.exe"`  


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1623)