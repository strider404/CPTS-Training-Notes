
2026-05-21 15:04

Tags: #escalation  

## Built-in Groups

- **Purpose:** Active Directory and Windows servers use *built-in groups* to delegate specific administrative tasks without granting full Domain Admin or Enterprise Admin rights.


- **Security Implication:** Excessive or leftover assignments to service accounts or users can be leveraged for privilege escalation.


- **High-Value Targets:** Backup Operators, Event Log Readers, DnsAdmins, Hyper-V Administrators, Print Operators, and Server Operators.


-  **Confirm Group Membership:**
    - Check local assignments: `net localgroup "<GROUP>"`
    - ![[Screenshot_20260521_155110.png]]
## Backup Operators Group & Privileges

- **Core Privileges:** Grants members `SeBackupPrivilege` and `SeRestorePrivilege`.


- **Bypass Capabilities:** Allows users to *traverse folders and copy files* by bypassing standard Access Control Lists (ACLs).


- **Technical Requirement:** Standard copy commands fail; data must be copied programmatically using the `FILE_FLAG_BACKUP_SEMANTICS` flag.

## Exploiting SeBackupPrivilege (Local Files)

- **Verification:** Check status using `whoami /priv` or PowerShell's `Get-SeBackupPrivilege`.
	- ![[Screenshot_20260521_150733.png]]



- **Tooling:** Import custom PoC libraries like `SeBackupPrivilegeUtils.dll` and `SeBackupPrivilegeCmdLets.dll`.
	- ![[Screenshot_20260521_150838.png]]


- **Activation:** Use `Set-SeBackupPrivilege` to enable it if disabled (may require an elevated prompt to bypass UAC).
	- ![[Screenshot_20260521_150918.png]]


- **Execution:** Use the `Copy-FileSeBackupPrivilege` cmdlet to copy protected files.
	- ![[Screenshot_20260521_151006.png]]


## Attacking Domain Controllers (NTDS.dit)

- **Access:** Backup Operators are permitted to *log locally* into a Domain Controller.


- **The Target:** `NTDS.dit`, the Active Directory database containing all NTLM hashes for the domain.


- **The Obstacle:** `NTDS.dit` is actively locked by the operating system and inaccessible to unprivileged users.


- **Shadow Copying:** Use the built-in `diskshadow.exe` utility to create a shadow copy of the `C:` drive and mount it to an unused letter (e.g., `E:`).
	- ![[Screenshot_20260521_151210.png]]


- **Copying the Target:** Retrieve the unlocked `ntds.dit` file from the newly exposed shadow volume.
	- ![[Screenshot_20260521_151242.png]]


- **Registry Hives:** Save the SYSTEM and SAM registry hives using the standard `reg save` command to obtain the boot key needed for decryption.
	- ![[Screenshot_20260521_151300.png]]


## Credential Extraction & Alternatives

- **Extraction Tools:** Process the extracted `NTDS.dit` and registry hives offline using tools like Impacket's `secretsdump.py` or the PowerShell `DSInternals` module.
	- ![[Screenshot_20260521_151339.png]]
	- ![[Screenshot_20260521_151403.png]]


- **Post-Exploitation:** Harvested hashes can be utilized in Pass-the-Hash attacks or cracked offline (e.g., with Hashcat) to compromise the domain.


- **Built-in Alternative:** Instead of using external PoC DLLs, you can leverage the native Windows `robocopy` utility with the `/B` flag to copy locked files in backup mode.
	- ![[Screenshot_20260521_151432.png]]
## References:

https://academy.hackthebox.com/app/module/67/section/601