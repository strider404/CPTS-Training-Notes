
2025-03-24 16:39

Tags: #windows  

## Registry

-  Windows Registry: a hierarchical ==database== storing system and application ==settings==

- Consist computer/user specific data 

- Accessing through `regedit`

- Organized into root keys (HKEYs), subkeys, and values.

- Root keys start with ==HKEY==

- Main root keys:
	- `HKEY_LOCAL_MACHINE (HKLM)` :  System-wide settings. Stored in C:\Windows\System32\Config\
	- `HKEY_CURRENT_USER (HKCU)`: User-specific settings. Stored in C:\Users\<USERNAME>\Ntuser.dat

- Types of value:

|**Value Type**|**Description**|
|---|---|
|**REG_BINARY**|Stores raw binary data.|
|**REG_DWORD**|32-bit number.|
|**REG_DWORD_LITTLE_ENDIAN**|32-bit number in little-endian format (default on Windows).|
|**REG_DWORD_BIG_ENDIAN**|32-bit number in big-endian format (used in some UNIX systems).|
|**REG_EXPAND_SZ**|String with unexpanded environment variables (e.g., `%PATH%`).|
|**REG_LINK**|Unicode string containing a symbolic link target path.|
|**REG_MULTI_SZ**|Multi-string sequence, each string is null-terminated.|
|**REG_NONE**|No defined value type.|
|**REG_QWORD**|64-bit number.|
|**REG_QWORD_LITTLE_ENDIAN**|64-bit number in little-endian format (default on Windows).|
|**REG_SZ**|Standard null-terminated string.|

## Run and RunOnce Registry Keys

- Run and RunOnce Registry Keys: contain grouped keys, subkeys, and values that support software and files loaded at system ==startup or user login==
	- Also called registry hives
	- Allow persistent or one-time execution of applications at startup

- Exist under both HKLM and HKCU:
	- HKLM\Software\Microsoft\Windows\CurrentVersion\Run
	- HKCU\Software\Microsoft\Windows\CurrentVersion\Run
	- HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
	- HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce


## Application Whitelisting

- Whitelisting: ==allows only approved applications== to run, reducing malware risks.

- Blacklisting: ==blocks known harmful applications== but allows everything else, making it less secure. 

- Whitelisting is recommended

- Whitelisting should be implemented in ==audit mode== to prevent blocking critical applications by mistake
	- Audit mode: nothing is restricted, just to see the impact of that policy

- Follow the zero-trust model


## AppLocker

- Microsoft’s ==application whitelisting== solution

- Allows administrators to control which apps and files users can run

- Supports rules for ==executables, scripts, DLLs, installers, and packaged apps==

- Rules can be created based on:
	- File attributes (publisher, product name, version, etc.).
	- File paths and hashes.

- Can be applied to **specific users or security groups**.

- Supports **Audit Mode** to test rules before enforcement.


## Local Group Policy

- Group Policy: used to ==configure system and security settings.==
	- Restricting applications
	- Enforcing security policies
	- Managing AppLocker policies

- In domain environments, settings are managed via **Group Policy Objects (GPOs)** from a **Domain Controller**.

- In non-domain setups, **Local Group Policy** is used.

- Domain vs non-domain: domain is when computers are centrally managed by a Domain Controller (DC) (like in workspace). Non-domain is when computer is independent 

- Access by `gpedit.msc`

- Registry vs Local Group Policy:
	- Registry is more powerful and also more risky
	- LGC is safer and more structured


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/462)