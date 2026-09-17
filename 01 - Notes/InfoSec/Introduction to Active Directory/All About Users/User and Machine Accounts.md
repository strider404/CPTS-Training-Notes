
2025-07-11 11:01

Tags: #ad  

## User Accounts

- **Purpose**: User accounts grant individuals or services the *ability to log on* to a system and access resources based on assigned rights.

- **Authentication & Access Token**: Upon login, the system verifies the user's credentials and creates an **access token**. This token contains the user's security identity (SID) and group memberships, and it is presented to processes to authorize actions.

- **Administration via Groups**: Users *can be assigned to groups*. Administrators can assign permissions to a group once, and all members inherit those rights. This simplifies the management of user privileges.


## Local Accounts

- Stored on a *specific server or workstation* and are not managed by a domain controller.

- Rights are confined to the local host only.

- **Default Local Accounts**:
	- **Administrator**: Has full control over the local system. It can be disabled or renamed but not deleted.
	  
	- **Guest**: Disabled by default; provides temporary, limited access.
	  
	- **SYSTEM (NT AUTHORITY\SYSTEM)**: The highest privilege account on a Windows host, used by the OS for internal functions. It has no user profile and cannot be added to groups.
	  
	- **Network Service**: A predefined local account for running services that need to present the computer's credentials to remote systems.
	  
	- **Local Service**: A predefined local account for running services with minimal local privileges and anonymous network credentials.

- **Domain Accounts**:
	- **Managed by Active Directory (AD)** and can be used to *log in to any machine joined to the domain.*
	  
	- Access to domain resources (file shares, printers, etc.) is determined by permissions granted to the user or their group memberships.
	  
	- **KRBTGT Account**: A *critical service account* for the Key Distribution Center (**KDC**) service. It is a *high-value target* for attackers, as compromising it can lead to *creating forged Kerberos tickets* (e.g., Golden Ticket attacks) and gaining complete domain control.


## User Naming Attributes

|                           |                                                                                                        |
| ------------------------- | ------------------------------------------------------------------------------------------------------ |
| `UserPrincipalName` (UPN) | The primary login name, conventionally the user's email address (e.g., `user@domain.com`).             |
| `ObjectGUID`              | A globally unique identifier for an object that never changes, even if the object is moved or renamed. |
| `SAMAccountName`          | The legacy login name for compatibility with older Windows versions (e.g., `DOMAIN\user`).             |
| `objectSID`               | The Security Identifier, a unique value that identifies a user or group during security interactions.  |
| `sIDHistory`              | Contains previous SIDs for a user object, typically after being migrated from another domain.          |


## Domain-joined vs. Non-Domain-joined Machines

- **Domain-Joined**:
	- Managed centrally by a Domain Controller (DC) via Group Policy.
	  
	- Allows for easy resource sharing across the enterprise.
	  
	- *Domain users can log in to any domain-joined machine.*


- **Non-Domain-Joined (Workgroup)**:
	- Managed locally by individual users.
	  
	- Resource sharing is more complex and typically limited to the local network.
	  
	- User accounts and profiles exist only on that specific host.
## References:

https://academy.hackthebox.com/module/74/section/704