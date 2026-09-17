
2026-06-17 09:22

Tags: 

## Targeted Kerberoasting (Privilege Escalation)

- **Initial Access:** You begin with compromised credentials for `mssqladm` (`DBAilfreight1!`).
    
- **Reconnaissance:** BloodHound reveals that `mssqladm` has **GenericWrite** privileges over the `ttimmons` user account.
	- ![[Pasted image 20260617092531.png]]
	    
- **The Attack:** * Using PowerView (`Set-DomainObject`), you leverage the GenericWrite privilege to place a fake Service Principal Name (SPN), such as `acmetesting/LEGIT`, on the `ttimmons` account.
    - With the SPN set, you use Impacket's `GetUserSPNs.py` to request the Kerberos TGS ticket for `ttimmons`.
        
    - You take the extracted hash offline and crack it using **Hashcat** against the `rockyou.txt` wordlist, successfully recovering `ttimmons`'s plaintext password.


## Group Delegation Exploitation

- **Reconnaissance:** Returning to BloodHound, you discover the newly compromised `ttimmons` user has **GenericAll** rights over the `SERVER ADMINS` group.
    
- **The Attack:** * Using PowerView (`Add-DomainGroupMember`), you abuse the GenericAll privilege to add `ttimmons` directly into the `SERVER ADMINS` group.

## The DCSync Attack (Domain Compromise)

- **Reconnaissance:** The `SERVER ADMINS` group natively possesses the necessary privileges to perform a DCSync attack (replicating directory changes).
    
- **The Attack:** * Now inheriting `SERVER ADMINS` privileges, you run Impacket's `secretsdump.py` targeting the Domain Controller.
    - This successfully dumps all NTLM password hashes from the NTDS.dit database, including the `Administrator` and `krbtgt` accounts, completing the domain takeover.

## Post-Exploitation & Client Reporting

- **Clean Up & Document:** Explicitly note all modifications in your report, such as the creation and subsequent deletion of the fake SPN on `ttimmons`.
    
- **Offline Password Cracking:** Crack the dumped NTDS database offline to provide the client with a comprehensive audit of their organization's password hygiene and strength metrics.
    
- **Provide Visual Evidence:** Take screenshots of an RDP session to the Domain Controller running simple commands (`hostname`, `whoami`, `ipconfig /all`). This is often more digestible for non-technical stakeholders than terminal output from `secretsdump`.
    
- **Test Blue Team Alerting:** Purposely create a loud event, such as adding a controlled user to the Domain Admin or Enterprise Admin groups. Check if their automated defenses or SOC catches the configuration change.
    
- **Give Kudos:** Always praise the client in the report if their defenses successfully detect or block your post-exploitation actions. Building goodwill is a crucial part of professional pentesting.
## References:

