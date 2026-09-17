
2025-04-15 14:27

Tags: #windows #shell 

## User Account

- Types of User Accounts:
	- **Service Accounts** – Run specific services.
	- **Built-in Accounts** – Default system accounts (e.g., Administrator, Guest).
	- **Local Users** – Exist only on a single machine.
	- **Domain Users** – Managed centrally through **Active Directory (AD)**, can access any domain-joined host.

- Built-in Accounts:

| **Account**           | **Description**                                                                                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Administrator`       | This account is used to ==accomplish administrative tasks== on the local host.                                                                                           |
| `Default Account`     | The default account is used by the system for ==running multi-user auth apps== like the Xbox utility.                                                                    |
| `Guest Account`       | This account is a limited rights account that ==allows users without a normal user account to access the host==. It is ==disabled== by default and should stay that way. |
| `WDAGUtility Account` | This account is in place for the ==Defender Application Guard==, which can sandbox application sessions.                                                                 |

## Active Directory Basics

- **AD** is a ==centralized directory service== managing users, computers, and resources in a Windows domain
	- Like a gatekeeper, anyone is part of the domain can access the resources, otherwise is blocked

- Can be administered by ==PowerShell's ActiveDirectory module==

## Local vs. Domain Users

- **Local Users**: Restricted to ==one== host.

- **Domain Users**: Can log into ==any== system in the domain; receive rights via domain policies and group memberships.


## User Groups

- Groups enable centralized permission control

- ==Instead of assigning permissions to each user==, groups allow simplified, scalable access control, especially important in large environments.


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1618)