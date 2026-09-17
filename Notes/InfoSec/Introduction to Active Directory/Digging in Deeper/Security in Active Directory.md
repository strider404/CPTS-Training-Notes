
2025-07-15 16:06

Tags: #ad  

## Security in Active Directory

- **Microsoft LAPS (Local Administrator Password Solution):** *Randomizes* and rotates local administrator passwords on Windows hosts to prevent lateral movement.

- **Audit Policies and Logging:** Configure *comprehensive logging and monitoring* to detect and react to unauthorized or suspicious activities, such as password spraying or changes to AD objects.

- **Group Policy Objects (GPOs):** Utilize GPOs to enforce a wide range of security settings, including:
	- **Account Policies:** Manage password requirements, account lockout, and Kerberos ticket settings.
	  
	- **Local Policies:** Control user rights, audit policies, and enable/disable/rename default accounts on specific computers.
	  
	- **Software/Application Control Policies (AppLocker):** Restrict which applications and scripts users can run.
	  
	- **Advanced Audit Policy:** Configure detailed logging for specific events like file access, policy changes, and privilege use.

- **Update Management (WSUS/SCCM):** Employ a centralized patch management solution to ensure timely *deployment of critical security updates* across all systems.

- **Group Managed Service Accounts (gMSA):** Use *domain-managed accounts* for services, which feature automatic management of long, complex passwords that are regularly changed.

- **Security Groups:** *Assign permissions to groups* rather than individual users to ensure granular, manageable access control based on roles.

- **Account Separation:** Require administrators to use a *standard, non-privileged account* for daily tasks and a separate, dedicated administrative account for privileged operations.

- **Password Policies & Multi-Factor Authentication (MFA):**
	- Enforce long passphrases over simple complex passwords.
	  
	- Use password filters to block common or weak passwords.
	  
	- Implement MFA, especially for Remote Desktop (RDP) access.

- **Limit Domain Admin Usage:** *Restrict Domain Administrator account logins* exclusively to Domain Controllers to prevent credential exposure on less secure workstations or servers.

- **Periodic Audits of Objects & Permissions:**
	- Regularly remove or disable stale/unused user accounts and computer objects.
	  
	- Routinely perform access control audits to enforce the principle of least privilege, ensuring users and groups only have the access they require.

- **Restricted Groups:** Use Group Policy to strictly control membership in highly privileged groups (e.g., local administrators, Domain Admins).
  
- **Limit Server Roles:** Do not install additional roles (e.g., IIS web server) on critical servers like Domain Controllers to reduce the attack surface.
  
- **Limit Local Admin and RDP Rights:** Tightly control which users have local administrator privileges or RDP access to machines to mitigate risks from a compromised low-privilege account.

## References:

https://academy.hackthebox.com/module/74/section/1282