
2025-07-09 15:55

Tags: #ad  

## Flexible Single Master Operation (FSMO) Roles

| **Roles**                  | **Description**                                                                                                                                                                                                                        |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Schema Master`            | This role manages the read/write copy of the *AD schema*, which defines all attributes that can apply to an object in AD.                                                                                                              |
| `Domain Naming Master`     | Ensures that any new domain added to the forest has a *unique name.*                                                                                                                                                                   |
| `Relative ID (RID) Master` | *Allocates blocks of unique Relative IDs (RIDs)* to Domain Controllers (DCs). These RIDs are combined with a domain SID to create a unique Security Identifier (SID) for every object.                                                 |
| `PDC Emulator`             | Acts as the authoritative DC for a domain. It handles *password* changes, *authentication* requests, manages Group Policy Objects (GPOs), and synchronizes *time* across the domain.                                                   |
| `Infrastructure Master`    | Responsible for *translating* object identifiers like GUIDs, SIDs, and Distinguished Names (DNs) between different domains within the same forest. If it fails, Access Control Lists (ACLs) may show unresolved SIDs instead of names. |


## Domain and Forest Functional Levels

- **Functional levels** dictate the available Active Directory Domain Services (AD DS) capabilities and *determine which Windows Server versions* can operate as Domain Controllers.

- **Domain Functional Levels**: Each level adds new features on top of the previous one.
    - **Windows 2000 Native**: Introduced universal groups, group nesting, and SID history.
        
    - **Windows Server 2003**: Added domain management tools, constrained delegation, and the `lastLogonTimestamp` attribute.
        
    - **Windows Server 2008**: Implemented Distributed File System (DFS) replication, AES encryption for Kerberos, and fine-grained password policies.
        
    - **Windows Server 2008 R2**: Introduced authentication mechanism assurance and Managed Service Accounts.
        
    - **Windows Server 2012**: Added Kerberos armoring and KDC support for claims.
        
    - **Windows Server 2012 R2**: Brought protections for the "Protected Users" group and Authentication Policies.
        
    - **Windows Server 2016**: Introduced new Kerberos features and enhanced credential protection.
        
- **Forest Functional Levels**: These introduce key capabilities across the entire forest.
    - **Windows Server 2003**: Enabled forest trusts and domain renaming.
        
    - **Windows Server 2008 R2**: Introduced the Active Directory Recycle Bin to restore deleted objects.
        
    - **Windows Server 2016**: Added Privileged Access Management (PAM) capabilities.
## Trusts

- A trust creates an **authentication link** between `forest-forest` or `domain-domain`, allowing users from one to access resources in the other.

- **Trust types:**
	- **Parent-child**: An automatic *two-way*, transitive trust between a parent and child domain in the same forest.
	  
	- **Cross-link**: A trust *between child domains* in different trees within the *same* forest to optimize authentication.
	  
	- **External**: A *non-transitive* trust connecting *two domains* in *separate* forests.
	  
	- **Tree-root**: A *two-way*, transitive trust between *the root of a forest* and *the root of a new domain tree* added to that forest.
	  
	- **Forest**: A *transitive* trust between the *root domains* of two different forests.

- **Trust Characteristics**:
	- **Transitivity**: A **transitive** trust *extends* to any other domains that the trusted domain trusts. A **non-transitive** trust is *limited* only to the specific domain it is established with.
	  
	- **Direction**: A **two-way** (bidirectional) trust allows users in both domains to access resources in the other. A **one-way** trust allows users in the _trusted_ domain to access resources in the _trusting_ domain, but not the reverse.



## References:

https://academy.hackthebox.com/module/74/section/1349