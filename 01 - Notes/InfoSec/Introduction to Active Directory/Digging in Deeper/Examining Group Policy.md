
2025-07-15 16:44

Tags: #ad  

## Group Policy

- **Definition:** Group Policy is a feature in Windows for the *centralized management and configuration of user and computer accounts* within an Active Directory (AD) domain.

- **Group Policy Objects (GPOs):** These are *virtual collections of settings*. Each GPO is assigned a unique identifier (GUID) and can be linked to AD containers such as Sites, Domains, or Organizational Units (OUs).

| **Level**                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Local Group Policy`       | **Scope:** Applied directly to an individual computer.<br>    <br>**Purpose:** Defines baseline settings for the local machine itself, independent of any domain.<br>    <br>**Precedence:** This is the first policy applied and has the lowest precedence. It will be overwritten by any conflicting policy from the Site, Domain, or OU levels.                                                                                                                                                                                                                                                        |
| `Site Policy`              | **Scope:** Applied to all users and computers within a specific physical location or network segment defined as an Active Directory "Site."<br>    <br>**Purpose:** Used for location-specific settings, such as configuring printers, shared drives, or access control rules relevant to a particular office or campus.                                                                                                                                                                                                                                                                                  |
| `Domain-wide Policy`       | **Scope:** Applied to all users and computers across the entire Active Directory domain.<br>    <br>**Purpose:** Enforces universal settings that should apply to everyone, such as the domain password complexity policy, a corporate desktop background, or a legal logon banner.                                                                                                                                                                                                                                                                                                                       |
| `Organizational Unit` (OU) | **Scope:** Applied to users and computers located within a specific OU or any of its nested sub-OUs.<br>    <br>**Purpose:** Provides the most granular control by applying role-specific or department-specific settings. For example, restricting application access for standard users while granting specific tool permissions to IT administrators within their respective OUs.<br>    <br>**Precedence:** This is the last policy applied and therefore has the highest precedence. A setting defined at the OU level will *override* a conflicting setting from the Domain, Site, or Local levels. |

- **Default Domain Controllers** is created by default and has the highest precedence


## GPO Application and Precedence

- **Order of Processing:** GPOs are processed in the following sequence:
	- **Local** Policy
	  
	- **Site** Policy
	  
	- **Domain** Policy
	  
	- **Organizational Unit (OU)** Policies (from parent OU to child OU)

![[Pasted image 20250715173305.png]]


- **Rule of Precedence:** Settings from GPOs processed later will **override settings from GPOs processed earlier**. For instance, a policy set at the OU level will take precedence over a conflicting policy set at the Domain level.


- **Managing Precedence:**
    - **Link Order:** When *multiple* GPOs are linked to a single OU, the GPO with the l*owest link order number (e.g., Link Order 1) has the highest precedence* and is processed last.
    - ![[Pasted image 20250715174011.png]]
      
    - **Enforced (No Override):** If a GPO link is set to "Enforced," its settings *cannot be overridden* by GPOs at lower levels in the hierarchy.
      
    - **Block Inheritance:** An OU can be configured to *block the application of GPOs from parent containers*. However, an "Enforced" GPO from a higher level will still apply, as **Enforced overrides Block Inheritance**.

- **Policy Refresh:** GPOs are not applied instantaneously. By default, they are refreshed every **90 minutes** (with a +/- 30-minute random offset) for client computers and every **5 minutes** for Domain Controllers.
  
- **Forcing Updates:** The command `gpupdate /force` can be executed on a client machine to manually trigger an immediate refresh of its Group Policy settings from the Domain Controller.

#### Security

- **Attack Vectors:** If an attacker gains permissions to modify a GPO, they can potentially achieve:
    - **Privilege Escalation:** By adding a controlled account to a privileged group (e.g., local administrators) on computers affected by the GPO.
      
    - **Lateral Movement:** By executing code or creating scheduled tasks on computers where the GPO applies.
      
    - **Persistence:** By creating accounts or running scripts that ensure their continued access to the network.

- **Vulnerability Analysis:** Misconfigurations in GPO permissions, such as allowing standard users to edit a GPO, create *exploitable attack paths*. Tools like **BloodHound** are specifically designed to identify and visualize these complex permission-based attack paths in Active Directory.

![[Pasted image 20250715174321.png]]


## References:

https://academy.hackthebox.com/module/74/section/706