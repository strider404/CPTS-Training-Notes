
2026-05-20 18:24

Tags: #escalation  

## Initial Enumeration

- **NT AUTHORITY\SYSTEM / LocalSystem:** The highest privilege level, used to run most Windows services.


- **Built-in Local Administrator:** Often enabled and frequently reused across multiple systems.


- **Local Administrators Group Members:** Any account in this group holds full administrative rights.


- **Privileged Domain Users:** Standard users or Domain Admins who have been added to the local admin group.

## System & OS Enumeration

- **OS Name and Version:** Helps identify legacy systems, determine PowerShell availability, and find version-specific public exploits.

- **`tasklist /svc`:** Maps running processes to their associated services to spot non-standard applications (like FileZilla) or active defenses (like Windows Defender).

- **`set`:** Displays environment variables to reveal system configuration.

- **PATH Variable (via `set`):** Highly critical—if writable directories are placed early in the PATH, they can be abused for DLL injection.

- **HOMEDRIVE / USERPROFILE (via `set`):** Reveals network shares and directories that may contain passwords, IT spreadsheets, or startup folders.

- **`systeminfo`:** Uncovers the OS build, system boot time (indicates patching frequency), VM status, network cards (useful for finding dual-homed hosts), and installed HotFixes.

- **`wmic qfe` / `Get-Hotfix`:** Lists specific security updates (KBs) to identify unpatched vulnerabilities.

- **`wmic product get name` / `Get-WmiObject -Class Win32_Product`:** Enumerates installed third-party software that may be vulnerable or contain stored credentials.

- **`netstat -ano`:** Displays active TCP/UDP connections to locate vulnerable services listening only on local ports. Can be used with the task manager to identify service's name.

## User & Group Enumeration

- **`query user`:** Identifies currently logged-in users and their activity status, which is crucial for evasive engagements.

- **`echo %USERNAME%`:** Confirms the current user context (you may already have a privileged account).

- **`whoami /priv`:** Lists specific user rights assigned to the account (look for highly abusable rights like `SeImpersonatePrivilege`).

- **`whoami /groups`:** Shows inherited rights from both local and Active Directory group memberships.

- **`net user`:** Lists all local accounts, helping identify credential reuse targets or interesting user profile directories.

- **`net localgroup`:** Reveals all local groups to help spot non-standard roles or overly permissive configurations.
    
- **`net localgroup administrators`:** Details the exact members of the most privileged local group.

- **`net accounts`:** Displays the local password policy, minimum length, and lockout thresholds.
## References:

