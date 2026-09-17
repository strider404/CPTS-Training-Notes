
2026-09-11 09:54

Tags: 

## Administrator

- Nmap
	- ![[Pasted image 20260911095619.png]]
		- Port 21, 53, 88, 135, 139, 389, 445, 464, 593, 636, 3268, 3269, 5985
		- FTP, DNS,LDAP, WinRM, 


- **Bloodhound**
	- bloodhound-python
	- ![[Pasted image 20260911101136.png]]
	- ![[Pasted image 20260911102123.png]]
	- Olivia has GenericAll over Michael, as shown in bloodhound
	- ![[Pasted image 20260911110909.png]]
	- Shadow Credential attack keep failing
	- ![[Pasted image 20260911110839.png]]
	- Force change his password to "password" through net rpc, and recheck with evil-winrm
	- ![[Pasted image 20260911111102.png]]
	- Michael has ForceChangePassword over Benjamin
	- ![[Pasted image 20260911111130.png]]
	- We change his password too
	- ![[Pasted image 20260911111214.png]]
	- He is in the non-default Share Moderators group
	- ![[Pasted image 20260911113413.png]]
	- evil-winrm failed
	- Because he is not in the Remote Management Users
	- ![[Pasted image 20260911113448.png]]
	- 

- Connect to ftp
	- ![[Pasted image 20260911113814.png]]
	- Get backup.psafe3
	- Crack that with hashcat: `hashcat -m 5200 Backup.psafe3 rockyou.txt`
	- Backup.psafe3:tekieromucho
	- Download Passwordsafe, open the file and get the passwords
	- emily:UXLCI5iETUsIBoFVTj8yQFKoHjXmb
	- alexander:UrkIbagoxMyUGw0aPlj9B0AXSea4Sw
	- emma:WwANQWnmJnGV07WQN8bMS7FMAbjNur


- Emily has GenericWrite over Ethan
	- ![[Pasted image 20260911142456.png]]
	- => We can Kerberoast him
	- ![[Pasted image 20260911142516.png]]
	- First, sync our time with the machine
	- ![[Pasted image 20260911142754.png]]
	- Perform targerted Kerberoast attack
	- `./targetedKerberoast.py -u emily -p UXLCI5iETUsIBoFVTj8yQFKoHjXmb -d administrator.htb -v`
	- Crack it with hashcat -m 13100
	- ethan:limpbizkit
	- ![[Pasted image 20260911144314.png]]
	- Ethan has GetChanges over the Domain Controller to perform DCSync 
	- Use secretsdump to perform a DCSync
	- ![[Pasted image 20260911145235.png]]
	- Connect to evil-winrm through PTH and get the flag

## References:

