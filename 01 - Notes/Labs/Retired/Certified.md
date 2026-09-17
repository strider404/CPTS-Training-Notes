
2026-09-08 10:15

Tags: 

## Certified

- Nmap
	- ![](Pasted%20image%2020260908101539.png)
	- ![](Pasted%20image%2020260908101552.png)
	- Port 53, 88, 135, 139, 389, 445, 464, 563, 636, 3268, 3269, 5985
	- As we can see, the Domain is `certified.htb`, and the DC is `dc01.certified.htb`


- Port 5985 (WinRM) is open => log into the provided account by `evil-winrm` with the provided credential: judith.mader:judith09
- ![](Pasted%20image%2020260908104243.png)
- Use bloodhound-python to collect everything about this domain
- ![](Pasted%20image%2020260908105222.png)
- Open bloodhound to ingest those files
- ![](Pasted%20image%2020260908105429.png)
- Found out that this judith user has the WriteOwner permission over the management group
- ![](Pasted%20image%2020260908105645.png)
- The **WriteOwner** permission allows a user to change the ownership of an object to a different user or principal, including one controlled by an attacker.
- And this Management Group has Generic Write over Management_SVC
- ![](Pasted%20image%2020260908110013.png)
-  **GenericWrite:** Allows writing to non-protected attributes (enables Kerberoasting or group modification).

- So we need to use WriteOwner to make us owner of this group, add us to the group, then use GenericWrite to access the management_svc account

- Change owner with `impacket's owneredit`
- ![](Pasted%20image%2020260908153610.png)
- Grant ourselves `FullControl` by `dacledit`
- ![](Pasted%20image%2020260908160018.png)
- Add ourselves to the group by `net rpc`
- ![](Pasted%20image%2020260908160828.png)
- Recheck
- ![](Pasted%20image%2020260908161101.png)

- We use the **Shadow Credential Attack**
	- **Prerequisite:** You need write access (`GenericAll`, `GenericWrite`, or `WriteProperty`) over the target object, and the DC must support PKINIT (Windows Server 2016+).
	  
	- **`msDS-KeyCredentialLink`**: An Active Directory attribute on user and computer accounts. It stores public keys used for passwordless login (specifically Windows Hello for Business). Whoever holds the matching private key can prove their identity.
	  
	- **Kerberos PKINIT**: An extension to Kerberos. Instead of encrypting an authentication timestamp with a password hash, the client signs the request using a private key (asymmetric cryptography).
    
	- **Step 1: Exploit Permissions**
	    - You control User A. User A has write rights (`GenericWrite` or `GenericAll`) over Victim B.
        
	    - You don't know Victim B's password.
        
	- **Step 2: Key Generation & Injection**
	    - You create a private/public key pair locally on your attack machine.
        
	    - Using your write access, you inject the **public key** into Victim B's `msDS-KeyCredentialLink` attribute in Active Directory.
        
	- **Step 3: Authenticate via PKINIT**
	    - You contact the Domain Controller and say: _"I am Victim B. Here is a Kerberos request signed with my private key."_
        
	    - The DC checks Victim B's `msDS-KeyCredentialLink`, sees your matching public key, verifies the signature, and hands you Victim B's **TGT**.
        
	- **Step 4: Dump Hash & Clean Up**
	    - You use the TGT to extract Victim B's actual **NT hash** (via UnPAC-the-hash).
        
	    - You delete the public key you added to `msDS-KeyCredentialLink` so the victim's account looks completely untouched.


- **Exploit**
	- Use `certipy`
	- ![](Pasted%20image%2020260909095359.png)`certipy-ad shadow auto -dc-ip 10.129.231.186 -u judith.mader@certified.htb -p judith09 -account management_svc -target certified.htb`
	- Got the time error, fix that by using rdate to align our time with the target
	- ![](Pasted%20image%2020260909095444.png)
	- ![](Pasted%20image%2020260909095515.png)
	- Got the NT hash: a091c1832bcdd4677c28b5a6a1295584
	- ![](Pasted%20image%2020260909100041.png)
	- Use PTH with evil-winrm


- Privilege Escalation
	- ![](Pasted%20image%2020260909104219.png)
	- Management_svc has GenericAll over CA_Operator
	- Use that to take over ca_operator
	- ![](Pasted%20image%2020260909110300.png)
	- b4b86f45c6018f1b664f70805f45d8f2
	- We use that credential to **enumerate vulnerabilities in Active Directory Certificate Service**
	- ![](Pasted%20image%2020260909110923.png)
	- ![](Pasted%20image%2020260909110935.png)
	- CA name: certified-DC01-CA
	- Certificate template: CertifiedAuthentication
	- Vulnerabilities: ESC9


- **ESC9**
	- **The Core Concept: Strong vs. Weak Mapping**
		- **Strong Mapping:** Normally, modern CAs embed the requester's SID (`objectSid`) into a certificate extension called `szOID_NTDS_CA_SECURITY_EXT`. When authenticating via PKINIT, the Domain Controller (DC) strictly checks this SID to verify who owns the certificate.
		    
		- **Weak Mapping:** If the certificate does not contain a SID extension, the DC falls back to matching the certificate's UPN/SAN to an Active Directory account’s `userPrincipalName` or `sAMAccountName` (provided strong enforcement is not set to full mode `2`).
	- **Prerequisites for ESC9**
		- **Vulnerable Template:**
		    - Has the flag `CT_FLAG_NO_SECURITY_EXTENSION` (`0x80000`) set in `msPKI-Enrollment-Flag`. This forces the CA **not** to embed the SID extension in issued certificates.
		    - Has Client Authentication EKU.
		    - Allows enrollment by low-privileged users.
        
		- **DC Configuration:** `StrongCertificateBindingEnforcement` registry key on the DC is set to `0` (disabled) or `1` (compatibility mode, allowing fallback to weak mapping).
    
		- **Write Permissions on a Puppet Account:** You have write rights (e.g., `GenericWrite`, `GenericAll`, or `WriteProperty` on `userPrincipalName`) over a regular target user (Account B).
	- How the Attack Works
		- **Step 1 (Change UPN):** You modify Account B's `userPrincipalName` (UPN) to match the username of a privileged target (e.g., `administrator@domain.local` or simply `administrator`).
    
		- **Step 2 (Enroll Certificate):** You request a certificate from the vulnerable template on behalf of Account B.
		    - Because the template has `CT_FLAG_NO_SECURITY_EXTENSION`, the CA builds the certificate containing the spoofed UPN but **omits Account B's SID**.
        
		- **Step 3 (Revert UPN):** You immediately change Account B’s UPN back to its original value to avoid collisions and detection.
    
		- **Step 4 (Authenticate via PKINIT):** You authenticate using the certificate. Because the certificate lacks a SID, the DC performs a weak lookup using the UPN embedded in the cert (`administrator`) and issues a Kerberos TGT for the **Domain Admin**.


- **Exploit ESC9**
	- First, change the UPN of ca_operator to Administrator
	- ![](Pasted%20image%2020260909112908.png)
	- Next, request a certificate
	- ![](Pasted%20image%2020260909113348.png)
	- Authenticate as Administrator and grab the hashes
	- ![](Pasted%20image%2020260909113747.png)
	- 0d5b49608bbce1751f708748f67e2d34
	- Use evil-winrm and get the flag
	- ![](Pasted%20image%2020260909113943.png)
## References:

