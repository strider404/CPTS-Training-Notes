
2026-05-21 10:06

Tags: #escalation  

## Overview

- **Privileges vs. Access Rights:** Privileges grant the ability to perform *system-wide operations* (e.g., shutting down, debugging, managing services). Access rights *grant or deny access* to specific securable objects (e.g., folders, files).


- **Access Tokens:** Granted upon logon, these store user and group privileges. Windows checks this token whenever a privileged action is attempted.


- **Attacker Goal:** Leverage built-in functionality or assigned privileges to escalate access to local administrator, Domain Admin, or SYSTEM.

## Windows Authorization Process

- **Security Principals:** Any entity authenticated by Windows (users, computers, processes, groups).


- **Security Identifier (SID):** A unique, permanent ID assigned to every security principal.


- **The Access Check:** When a user attempts to access an object, Windows compares the user's access token (containing their SID and privileges) against the **Access Control Entries (ACEs)** in the object's security descriptor to instantaneously grant or deny access.

![[Pasted image 20260521100951.png]]


## High-Value Groups for Privilege Escalation

- **Server Operators:** Can modify services, access SMB shares, and back up files.
    
- **Backup Operators:** Can log onto Domain Controllers (DCs) locally, copy the SAM/NTDS database, and access the DC file system via SMB. Essentially Domain Admins.
    
- **Print Operators:** Can log onto DCs locally and load malicious drivers.
    
- **Hyper-V Administrators:** Virtualization admins with authority that often equates to Domain Admin status.
    
- **Account Operators:** Can modify non-protected domain accounts and groups.
    
- **Schema Admins:** Can backdoor AD by modifying the schema structure and default object Access Control Lists (ACLs).
    
- **DNS Admins:** Can load malicious DLLs on a DC or create malicious WPAD records.

## Key User Rights Assignments

- **SeBackupPrivilege & SeRestorePrivilege:** Allows bypassing file, directory, and registry permissions to back up or restore the system.
    
- **SeTakeOwnershipPrivilege:** Allows the user to take ownership of any securable object, bypassing standard restrictions.
    
- **SeDebugPrivilege:** Allows attaching to or opening any process, granting access to critical operating system components.
    
- **SeImpersonatePrivilege:** Allows programs to impersonate another authenticated client and act on their behalf.
    
- **SeLoadDriverPrivilege:** Allows dynamically loading/unloading device drivers, which execute as highly privileged code.
    
- **SeTcbPrivilege:** Allows a process to act as part of the operating system to assume any user identity.

## Enumeration & Privilege States

- **Command:** Running `whoami /priv` lists all assigned user rights for the current session.
    
- **User Account Control (UAC):** Standard user sessions severely restrict visible and usable privileges. An elevated administrative console is required to see and use the full list of admin rights.
    
- **Disabled State:** If a privilege is listed as **Disabled**, it means the account possesses the right, but it is currently inactive. It must be manually enabled (typically via PowerShell scripts) before it can be used in an exploit.
## References:

