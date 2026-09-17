
2026-06-13 10:47

Tags: 

## Active Directory Enumeration (BloodHound)

- Using the previously discovered `hporter` credentials, the attacker uses the `DEV01` host as a staging area to map the domain.
	- **Collection:** The `SharpHound.exe` collector is executed on `DEV01` to gather all Active Directory object data.
	    
	- **Analysis:** The ingested data in the BloodHound GUI reveals that `hporter` has **ForceChangePassword** rights over the `ssmalls` user.
	    
	- **Finding:** BloodHound also reveals that all Domain Users have RDP access to `DEV01`, which is flagged as a medium-risk finding (Excessive Active Directory Group Privileges).

## Exploiting Object Control (Password Reset)

- To exploit the BloodHound finding and take over the `ssmalls` account, the attacker uses an RDP session.
	- **Local Port Forwarding:** An SSH tunnel is created to forward local port `13389` to `172.16.8.20:3389` (DEV01).
	    
	- **Execution:** After connecting via `xfreerdp` as `hporter`, the attacker uses the `PowerView` PowerShell module to forcefully reset the `ssmalls` password to `Str0ngpass86!`.

## Share Hunting & Credential Harvesting

- With the newly acquired `ssmalls` credentials, the attacker systematically hunts through SMB shares for sensitive data using `CrackMapExec` (NetExec) and `smbclient`.

|**Target Share**|**File Found**|**Discovered Credential / Loot**|
|---|---|---|
|`Department Shares`|`SQL Express Backup.ps1`|Hardcoded password for the **`backupadm`** user.|
|`SYSVOL`|`adum.vbs`|Old legacy credentials (`account:L337^p@$$w0rD`).|

## Broadening the Attack Surface (Findings)

- The lecture highlights several other AD attacks that, while not providing the final path to Domain Admin in this lab, yield critical findings for a penetration testing report:
	- **Kerberoasting:** Enumerating SPNs with PowerView and cracking the hash for the `backupjob` account (Weak Kerberos Auth).
	    
	- **Password Spraying:** Using `Invoke-DomainPasswordSpray` with the password `Welcome1` to compromise two low-level accounts (Weak AD Passwords).
	    
	- **Information Disclosure:** Discovering the `frontdesk` user's password stored in plain text within their AD Account Description field.

## Pivoting to MS01 & Local Privilege Escalation

- Using the harvested `backupadm` credentials, the attacker successfully authenticates to the last unknown host, `172.16.8.50` (`MS01`), via `evil-winrm`.

- **Privilege Escalation Steps:**
	1. **Unattend.xml:** Searching the `C:\panther` directory reveals an `unattend.xml` file containing local credentials for `ilfserveradm:Sys26Admin`
	    
	2. **RDP Access:** The `ilfserveradm` user is not an administrator but has RDP rights.
	    
	3. **Exploiting Sysax:** Enumeration via RDP reveals vulnerable "SysaxAutomation" software.
	    
	4. **SYSTEM Execution:** The attacker abuses a Sysax Scheduled Task (which defaults to running as `NT AUTHORITY\SYSTEM`) to execute a malicious `.bat` file, successfully adding `ilfserveradm` to the local Administrators group.


## Post-Exploitation & Pillaging MS01

- With local administrator rights on `MS01`, the attacker focuses on extracting high-value credentials from the system's memory and registry.

- **LSA Secrets:** Using `Mimikatz` (elevated to a SYSTEM token), the attacker dumps LSA secrets and finds a plaintext `DefaultPassword` (`DBAilfreight1!`).
    
- **Registry Query:** Because the LSA dump did not show the username, the attacker queries the `Winlogon\DefaultUserName` registry key to reveal the associated account: **`mssqladm`**.
    
- **Traffic Sniffing:** Finally, running `Inveigh` on the host captures an NTLMv2 hash for the user `mpalledorous` connecting over SMB.
## References:

