
2025-02-22 16:03

Tags: #linux #bash 

## Permission Management

- ==3 main types== of permission:
	- r: Read
	- w: Write
	- x: Execute

- Execute:
	- In directories: allow to ==traverse== to that directory
	- In files: allow to ==execute== the files

- Write: modify contents

- Permission can be set to ==owner, group or others==
![[Pasted image 20250222161127.png]]


## SUID & SGID

- Set User ID (`SUID`) & Set Group ID (`SGID`) allow user to ==run the program with the privileges of other group== (Ex: user can perform tasks with the permission of owner or group owner)

- Can be seen by the =='s'== in the common position of the 'x' (if it's SUID so it will be in the 'x' of owner, for SGID it's the group's 'x' )

- Octal number for SUID is 4, SGID is 2 (Ex: `chmod 2775 folder2`)

- Capitalized (S) means the execute permission is not given

## Sticky Bit

- Sticky Bit ==ensuring only certain individuals (the root or the owner) can modify or delete files==

- Can be seen by the =='t'== in the common position of the 'x' of the others group

- Octal number for Sticky Bit is 1 (Ex: `chmod 1775 folder2`)

- Capitalized (T) means the execute permission is not given

![[Pasted image 20250222165810.png]]

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/83)