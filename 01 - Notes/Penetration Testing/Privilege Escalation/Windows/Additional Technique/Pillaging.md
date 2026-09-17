
2026-05-27 11:00

Tags: #escalation 

## Pillaging

- **Pillaging** is the post-exploitation process of *extracting sensitive information* from a compromised system to aid in lateral movement, privilege escalation, or fulfilling specific assessment objectives. Valuable data includes credentials, corporate blueprints, infrastructure details, and configuration files.

- ![[Pasted image 20260527110249.png]]
## Data Sources and Installed Applications

- Identifying **installed software** is critical to understanding the target environment. Standard methods include checking `C:\Program Files` or querying the Windows Registry via PowerShell for granular details.
	- ![[Pasted image 20260527110300.png]]
	- ![[Pasted image 20260527110311.png]]


- **Key locations and services to investigate include:**
	- Installed applications and background services
	    
	- Directory Services (Active Directory, Azure AD)
	    
	- File shares, databases, and backup systems
	    
	- Web browsers and Instant Messaging (IM) clients
	    
	- Source Code Management and Deployment services


## Abusing Remote Management Tools: mRemoteNG

- **mRemoteNG** is a popular *remote connection manager* that often stores plaintext or weakly encrypted credentials.


- **Configuration File:** Located at `%USERPROFILE%\APPDATA\Roaming\mRemoteNG\confCons.xml`.
	- ![[Pasted image 20260527110325.png]]


- **Default Master Password:** The default encryption uses a hardcoded master password (**mR3m**).


- **Decryption:** The Python script `mremoteng_decrypt.py` can decrypt credentials using the default password.
	- ![[Pasted image 20260527110354.png]]
	- With master password:
	- ![[Pasted image 20260527110528.png]]


- **Cracking:** If a custom master password is set, the same script can be combined with wordlists and a bash loop to brute-force the `Protected` attribute or the `Password` string.
	- ![[Pasted image 20260527110424.png]]
	- ![[Pasted image 20260527110510.png]]


## Exploiting Instant Messaging (IM) Clients

|**Browser**|**Database Location**|**Encryption**|**Extraction Method**|
|---|---|---|---|
|**Firefox**|`%APPDATA%\Mozilla\Firefox\Profiles\[random].default-release\cookies.sqlite`|None (Standard SQLite)|`cookieextractor.py`|
|**Chromium**|`%LOCALAPPDATA%\Google\Chrome\User Data\Default\Network\Cookies`|DPAPI (Tied to user/host)|`Invoke-SharpChromium`|

## Clipboard Monitoring

- Because password managers negate the effectiveness of traditional keystroke logging, monitoring the system **clipboard** is highly effective for capturing copied passwords, 2FA soft tokens, and sensitive URLs.

- **Execution:** PowerShell scripts like `Invoke-ClipboardLogger` hook into the system to output clipboard contents in real-time.
	- ![[Pasted image 20260527111724.png]]
	    
- **Use Case:** Ideal for grabbing credentials as an administrator copies them from a vault to a login prompt.

## Attacking Backup Servers: Restic

- **Backup** systems are high-value targets because they typically run with **local administrative privileges** and store snapshots of the entire environment. Restic is a modern backup tool used across multiple OS environments.


- Restic Operational Workflow:
	- **Initialization:** Requires the `RESTIC_PASSWORD` environment variable to unlock or initialize a repository.
    
	- **Backups:** Commands like `restic.exe -r [repo] backup [target]` create the snapshot.
    
	- **Bypassing File Locks:** Adding the `--use-fs-snapshot` flag utilizes the Volume Shadow Copy Service (VSS) to back up files actively in use by the OS.
    
	- **Restoration:** Attackers can list backups with the `snapshots` command and use the `restore` command to extract them to a readable directory.


- **High-Value Backup Targets:**
	- **Windows:** SAM and SYSTEM registry hives (for local credential hashes), `web.config` files, and application databases.
	    
	- **Linux:** `/etc/shadow` (password hashes), `/etc/passwd`, and `.ssh` directories (private keys).
## References:

