
2025-07-15 15:47

Tags: #ad  

## Rights vs. Privileges

- **Rights**: Permissions assigned to users or groups to *access an object* (e.g., a file or folder).

- **Privileges**: Permissions granted to a user to *perform a specific system-level action* (e.g., reset passwords, shut down a system).

## Built-in Active Directory Groups

- **Important Groups:**
	- `Administrators`/`Domain Admins`/`Enterprise Admins`: Provide *unrestricted access* to a computer, domain, or entire forest, respectively.
    
	- `Backup Operators`: Can *bypass file permissions to back up and restore any file*, including sensitive credential databases like the SAM hive and `NTDS.dit`. Should be considered equivalent to Domain Admins.
    
	- `Server Operators`: Can *administer domain controllers.*
    
	- `Print Operators`: Can log on to *domain controllers* and potentially load malicious printer drivers to escalate privileges.
    
	- `DnsAdmins`: If a DNS server role is on a domain controller, membership can be abused for privilege escalation.
    
	- `Schema Admins`: Can *modify the AD schema*, which defines all objects in the directory.


## User Rights Assignment and Exploitable Privileges

- **Administrators** can *assign specific privileges* to user accounts, often via Group Policy Objects (GPOs). Certain privileges are particularly dangerous if misassigned.

- **Key Privileges Exploitable for Escalation:**
	- `SeBackupPrivilege`: Allows *backing up sensitive system files* (`SAM`, `SYSTEM`, `NTDS.dit`) to extract credentials offline.
	  
	- `SeDebugPrivilege`: Allows *attaching to and inspecting the memory of other processes*, such as `LSASS`, to dump credentials.
	  
	- `SeImpersonatePrivilege`: Allows a *process to impersonate other security tokens*, which can be used with tools like JuicyPotato to escalate to `NT AUTHORITY\SYSTEM`.
	  
	- `SeTakeOwnershipPrivilege`: Allows *a user to take ownership of objects*, bypassing access controls on files and other resources.
	  
	- `SeLoadDriverPrivilege`: Allows *loading and unloading of kernel-mode drivers,* which can be used to compromise the system.


#### Viewing Privileges and User Account Control (UAC)

- The command `whoami /priv` can be used on a host to display the privileges assigned to the current user's token.
  
- **User Account Control (UAC)** is a security mechanism that *limits the privileges of a process by default*, even for administrative accounts.
  
- An **administrator** running in a _non-elevated_ command prompt will have a restricted set of privileges. To access the full set of assigned privileges (e.g., `SeDebugPrivilege`), the process must be run in an _elevated_ context (e.g., "Run as administrator").

## References:
https://academy.hackthebox.com/module/74/section/709
