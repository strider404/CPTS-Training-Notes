
2025-07-09 11:12

Tags: #ad  

## Active Directory Objects

![[Pasted image 20250709111259.png]]


#### User

- **Type**: Leaf Object, Security Principal

- **Description**: Represent user accounts in the organization

- **Security Note**: They are a *primary target* for attackers, as even a low-privileged account can be used for enumeration and privilege escalation.

- **Attributes**: Display name, login times, password data, email, and potentially over 800 others.


#### Contact

- **Type**: Leaf Object, *Not* a Security Principal.

- **Description**: Represents *external users* (e.g., a third-party vendor) for informational purposes.

- **Attributes**: Name, email address, phone number.


#### Printers

- **Type**: Leaf Object, **Not** a Security Principal.

- **Description**: Points to a printer accessible on the AD network.

- **Attributes**: Printer name, driver information, port number.


#### Computers

- **Type**: Leaf Object, Security Principal.

- **Description**: Represents any workstation or server joined to the domain.

- **Security Note**: A *prime target* for attackers. Gaining administrative access (as `NT AUTHORITY\SYSTEM`) provides rights similar to a domain user, enabling network enumeration.


#### Shared Folders

- **Type**: **Not** a Security Principal.

- **Description**: Points to a shared folder on a specific computer.

- **Security Note**: Access is managed through *permissions* which can range from being *open* to everyone to being *restricted* to specific users/groups.

#### Groups

- **Type**: Container Object, Security Principal.

- **Description**: Used to manage permissions and access for multiple objects at once. Can contain users, computers, and other groups.

- **Security Note**: "Nested groups" (a group within another group) can lead to unintended access rights, a common vector for attackers to exploit. Tools like **BloodHound** are used to identify these attack paths.


#### Organizational Units (OUs)

- **Type**: Container Object.

- **Description**: A *container* used by administrators to *organize similar objects* for easier management, delegation of administrative tasks (e.g., password resets), and *application of Group Policy.*


#### Domain

- **Description**: The foundational structure of an AD network that contains all other objects. Each domain has its own database and policies.

#### Domain Controllers (DCs)

- **Description**: The *core servers* of an AD network. They handle authentication, enforce security policies, and store all object information for the domain.

#### Sites

- **Description**: A *collection of computers* across one or more subnets connected by high-speed links, used to manage and optimize replication traffic between Domain Controllers.

#### Built-in

- **Description**: A container that holds the *default, pre-defined groups* created when a new AD domain is set up.


#### Foreign Security Principals (FSPs)

- **Description**: Placeholder objects that represent a *security principal* (user, group, etc.) from a *trusted external forest*. They are created automatically when a foreign object is added to a group in the current domain, holding the foreign object's SID to resolve its identity across the trust.

## References:

https://academy.hackthebox.com/module/74/section/1348