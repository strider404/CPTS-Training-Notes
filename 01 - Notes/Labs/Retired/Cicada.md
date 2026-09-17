
2026-08-13 14:50

Tags: 

## Cicada

- Nmap
	- ![](Pasted%20image%2020260813145013.png)
	- ![](Pasted%20image%2020260813145030.png)
	- Port 53,88,135,139,389,445,464,593,636,3268,3269,5985

- Utilize smbclient to list shares that are accessible with the guest account
	- ![](Pasted%20image%2020260813145533.png)
	- Get the Notice from HR.txt file in the HR share
	- ![](Pasted%20image%2020260813145555.png)
	- Cicada$M6Corpb*@Lp#nZp!8


- **RID brute**
	- In Windows Active Directory, every security principal (users, groups, computer accounts) is assigned a unique **Security Identifier (SID)**
	- This is SID
	- ![](Pasted%20image%2020260813151750.png)
	- A SID consists of a domain prefix and ends with a numerical **Relative Identifier (RID)**
	- In this case the RID is 1601
	- Standard default RIDs include:
	- `500`: Administrator
	- `501`: Guest
	- `502`: krbtgt
	- User accounts created later receive sequentially assigned RIDs starting at `1000` (e.g., `1000`, `1104`, `1601`)


- RID brute with nxc
	- `nxc smb 10.10.11.35 -u '.' -p '' --rid-brute`
	- NetExec iterates sequentially through a range of RIDs (e.g., `500` through `2000` or higher) over MSRPC/SAMR
	- Under the Hood
	- To illustrate how it works under the hood, IppSec connects via `rpcclient`:
	- `rpcclient -U 'cicada.htb/' 10.10.11.35`
	- He executes `lookupsids` against known SIDs/RIDs:
		- Passing `S-1-5-21-...-500` returns `CICADA\Administrator`
		- Changing the last number to `1601` returns `CICADA\emily.oscars`
		- ![](Pasted%20image%2020260813152045.png)
		- **RID Brute-Forcing** simply automates querying these numerical endpoints step-by-step; whenever the response isn't `NT_STATUS_NONE_MAPPED` or `unknown`, it records the discovered username
	- **Results**
		- ![](Pasted%20image%2020260813152113.png)
		- Write a script to filter out only the usernames
		- `grep '(SidTypeUser)' names.txt | awk -F'\\\\' '{print $2}' | awk '{print $1}'`
	- Brute force with the list, found 1 valid credential
	- ![](Pasted%20image%2020260813153125.png)
	- cicada.htb\michael.wrightson:Cicada$M6Corpb*@Lp#nZp!8
	- This guy cannot access Dev share
	- ![](Pasted%20image%2020260813153552.png)


- Enumerate domain users with nxc and authenticated credential (this time will get more info)
	- ![](Pasted%20image%2020260813153756.png)
	- This david guy left his password in the description loool
	- `david.orelious:aRt$Lp#7t*VQ!3`
	- ![](Pasted%20image%2020260813153941.png)
	- He can read the Dev share
	- ![](Pasted%20image%2020260813154051.png)
	- Backup_script.ps1
	- ![](Pasted%20image%2020260813154128.png)
	- Another cred: `emily.oscars:Q!3@Lp#M6b*7t*Vt`
	- Connect to her with evil-winrm and get the flag
	- ![](Pasted%20image%2020260813154319.png)


- **Escalation**
	- ![](Pasted%20image%2020260813154809.png)
	- This user has **SeBackupPrivilege**
	- Allows *backing up sensitive system files* (`SAM`, `SYSTEM`, `NTDS.dit`) to extract credentials offline.
	- Attempted to dump SAM, SYSTEM and SECURITY hives, but the SECURITY one failed
	- ![](Pasted%20image%2020260813155505.png)
	- ![](Pasted%20image%2020260813155859.png)
	- Dump it with secretsdump
	- Pass the hash, and get the root
	- ![](Pasted%20image%2020260813160241.png)

## References:

