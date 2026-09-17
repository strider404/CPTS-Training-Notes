
2025-03-24 10:31

Tags: #windows  

## Windows Security

 - Windows has a lot of built-in applications and configuration options -> the attack surface is large

## Security Identifier (SID)

- Every security principle is given a SID by the system (string)
	- If there are 2 users have the same name -> Windows can still distinguish them

- To identify the authorities of the users

![[Pasted image 20250324104204.png]]

- For other users: `Get-WmiObject win32_useraccount`
- Breakdown:

| **Number**                       | **Meaning**          | **Description**                                                                                                                                                                                        |
| -------------------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| S                                | SID                  | Identifies the string as a SID.                                                                                                                                                                        |
| 1                                | Revision Level       | To date, this has never changed and has always been `1`.                                                                                                                                               |
| 5                                | Identifier-authority | A 48-bit string that identifies the ==authority== (the computer or network) that created the SID.                                                                                                      |
| 21                               | Subauthority1        | This is a variable number that identifies the ==user's relation or group== described by the SID to the authority that created it. It tells us in what order this authority created the user's account. |
| 2792878555-4069422439-2473165106 | Subauthority2        | Tells us which ==computer== (or domain) created the number                                                                                                                                             |
| 1001                             | Subauthority3        | The RID that ==distinguishes== one account from another. Tells us whether this user is a normal user, a guest, an administrator, or part of some other group                                           |

## Security Accounts Manager (SAM) and Access Control Entries (ACE)

- Security Accounts Manager (SAM) assigns the rights for a network

- The access rights themselves are managed by Access Control Entries (ACE) in Access Control Lists (ACL)
	- Which users, groups, processes have access / execute files

- 2 types of ACLs:
	- Discretionary Access Control List (DACL)
	- System Access Control List (SACL)


## User Account Control (UAC)

 - User Account Control (UAC): ==prevent malware or unauthorized software== from making system-wide changes by requiring ==administrator approval==
	 - Remember the pop-ups when you install a pirated game?

![[Pasted image 20250324110435.png]]

- If the users don't have the rights to execute it -> they will be asked for admin's password

- How it works:
![[Pasted image 20250324115330.png]]


- Consent Prompt or Automatic Elevation
	- Consent Prompt:
		- If configured, Windows prompts the user for approval (or an admin password).
		- The user can Allow or Deny.
	- Automatic Elevation:
		- Under some policies (e.g., for trusted Microsoft executables, or in silent-elevation environments), Windows may automatically grant elevation without a visible prompt.

- UAC Slider:
	- ![[Pasted image 20250324114817.png]]

- Secure Desktop ON vs OFF:
	- ![[Pasted image 20250324115117.png]]


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/462)