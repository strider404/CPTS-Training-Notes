
2025-07-04 16:10

Tags: #ad  

## Core Components

- **Object:** Any resource in Active Directory, such as users, computers, printers, or Organizational Units (OUs).

- **Attributes:** Characteristics that define an object. For example, a user object has attributes like `displayName` and `givenName`.

- **Schema:** The *blueprint* for the Active Directory environment. It defines the types of objects that can exist and their associated attributes. (like a *class*)

## Logical Structure

- **Domain:** A logical grouping of objects like users and computers. It can be seen as a *boundary* for administration.
  
- **Tree:** A *collection of one or more domains* that share a *contiguous namespace*. A parent-child trust is automatically created between domains in a tree.
  
- **Forest:** The top-level container in Active Directory, consisting of one or more trees. It represents the complete AD instance.

## Organizational & Hierarchical Elements

- **Container:** An object that can hold other objects.

- **Leaf:** An object that cannot contain other objects and exists at the end of a hierarchy branch.

- **Organizational Unit (OU):** A specialized container used to organize objects within a domain for easier administration and application of Group Policy

## Object Identification

- **Distinguished Name (DN):** The unique, full path to an object in the directory. It must be *unique across the entire directory.*
	- _Example:_ `inlanefreight.local/Users/Sales/Managers/BJones`

- **Relative Distinguished Name (RDN):** The part of the DN that is *unique within its parent container.*
	- _Example from image:_ `BJones` is the RDN within the `Managers` OU.

- **Globally Unique Identifier (GUID):** A *128-bit value* assigned to an object upon creation that *never changes* and is *unique* across the entire forest.
	- Used to distinguish objects

- **Security Identifier (SID):** A *unique* ID used to identify a security principal (user, group, computer). It is used for access control.
	- Use one time only
	- Used to check if user/ group has the rights to access that data or not

- **Service Principal Name (SPN):** *uniquely identifies a service* instance. Used in Kerberos to associate an instance of a service with a logon account.

- **sAMAccountName:** A user's logon name (e.g., `bjones`) that must be unique within the domain and is 20 characters or less.

- **userPrincipalName (UPN):** A user-friendly logon name in an email format (e.g., `bjones@inlanefreight.local`).

- **Fully Qualified Domain Name (FQDN):** The complete domain name for a specific host, such as `DC01.INLANEFREIGHT.LOCAL`.
	- Written in format `[host name].[domain name].[tld]`

## Operational Roles & Services

- **Domain Controller (DC):** A *server running Active Directory Domain Services (AD DS)* that is responsible for responding to security authentication requests (e.g., logins, permission checks) within a domain.

- **Flexible Single Master Operation (FSMO) Roles:** Five specialized roles assigned to *Domain Controllers (DCs)* to prevent conflicts and ensure consistency in a multi-DC environment.
	- `Schema Master` and `Domain Naming Master` (one of each per forest)
	- `Relative ID (RID) Master` (one per domain)
	-  `Primary Domain Controller (PDC) Emulator` (one per domain)
	- `Infrastructure Master` (one per domain)

- **Global Catalog (GC):** A *DC* that stores a *full copy of all objects in its own domain* and a partial copy of all objects from other domains in the forest, enabling forest-wide searches and authentication.

- **Read-Only Domain Controller (RODC):** A DC with a *read-only copy* of the AD database, often used in less secure locations.

- **Replication:** The process of synchronizing AD data between Domain Controllers to ensure all DCs have up-to-date information.


## Security & Access Control

- **Security Principal:** Any entity that *can be authenticated* by the system, such as a user or computer account.

- **Access Control Entry (ACE):** An entry in an ACL that *specifies the access rights* *(allow, deny, audit)* for a particular trustee (user or group).

- **Access Control List (ACL):** A *list* of *permissions* *(Access Control Entries)* attached to an object.

- **Discretionary Access Control List (DACL):** DACLs define which security principles are granted or denied access to an object; it contains a list of ACEs.

- **System Access Control List (SACL):** The part of an object's security descriptor that controls auditing of access attempts.

- **AdminSDHolder:** A special container object whose ACL serves as a template for protected groups in AD (like Domain Admins). The `SDProp` process periodically enforces this template on protected members.

- **adminCount:** An attribute (value of `1`) that indicates a user is or was a member of a protected group.

- **sIDHistory:** An attribute that stores previous SIDs for a migrated user or group to maintain access to old resources.

## Data Storage & Management

- **NTDS.DIT:** The *core database file* for Active Directory, located on Domain Controllers. It stores *all AD objects*, including user *password hashes.*
  
- **SYSVOL:** A shared folder on every DC that stores public files for the domain, such as Group Policy templates and logon scripts.
  
- **Tombstone:** A container for *deleted* AD objects. Objects are held here for a specific period (Tombstone Lifetime) before being permanently removed, allowing for recovery.
  
- **AD Recycle Bin:** A feature (introduced in Windows Server 2008 R2) that enhances the tombstone functionality by preserving most attributes of deleted objects, making restoration easier.
  
- **Group Policy Object (GPO):** A collection of *settings* that control the working environment of *user and computer accounts*

## Management Tools

- **Active Directory Users and Computers (ADUC):** A standard GUI tool for day-to-day management of users, groups, and computers.
  
- **ADSI Edit:** A more advanced GUI tool that provides low-level access to all objects and attributes in AD.

## Legacy Protocols

- **MSBROWSE:** An obsolete protocol used in early Windows networks for Browse and locating network resources. It has been replaced by protocols like SMB and CIFS.
  
## References:

https://academy.hackthebox.com/module/74/section/1347