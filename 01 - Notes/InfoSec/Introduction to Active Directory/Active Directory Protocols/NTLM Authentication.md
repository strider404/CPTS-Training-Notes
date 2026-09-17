
2025-07-10 16:47

Tags: #ad  

## NTLM Authentication

- Active Directory (AD) uses several authentication methods besides Kerberos and LDAP, including **LM**, **NTLM**, **NTLMv1**, and **NTLMv2**.

- It is crucial to differentiate between the **hash types** (LM, NT) and the **authentication protocols** (NTLMv1, NTLMv2) that use them.


#### Hashing vs Encryption

- **Hashing**: *cannot* be transferred back into the original. Used in authentication/verification

- **Encryption**: *can* be transferred back into original using the key. Used to hide the contents

#### Hash Protocol Comparison

| **Hash/Protocol** | **Cryptographic technique**                          | **Mutual Authentication** | **Message Type**                | **Trusted Third Party**                         |
| ----------------- | ---------------------------------------------------- | ------------------------- | ------------------------------- | ----------------------------------------------- |
| `NTLM`            | Symmetric key cryptography                           | No                        | Random number                   | Domain Controller                               |
| `NTLMv1`          | Symmetric key cryptography                           | No                        | MD4 hash, random number         | Domain Controller                               |
| `NTLMv2`          | Symmetric key cryptography                           | No                        | MD4 hash, random number         | Domain Controller                               |
| `Kerberos`        | Symmetric key cryptography & asymmetric cryptography | Yes                       | Encrypted ticket using DES, MD5 | Domain Controller/Key Distribution Center (KDC) |

## LAN Manager (LM) Hash

- **Oldest Method:** The original password hashing mechanism for Windows, introduced in 1987.

- **Storage:** Located in the SAM database on local machines or the NTDS.DIT database on Domain Controllers.

- **Major** **Weaknesses**:
	- Passwords are converted to uppercase and limited to 14 characters.
    
	- The password is split into two 7-character chunks, which are hashed separately. This significantly reduces the effort needed to brute-force the hash.
	  
	- A password of 7 characters or less results in a constant, easily identifiable second half of the hash.

- Disabled


## NT Hash (NTLM)

- **Modern Standard:** Used in current Windows systems.

- **Process**: It is a challenge-response protocol. The client sends a NEGOTIATE_MESSAGE, the server replies with a CHALLENGE_MESSAGE, and the client authenticates with an AUTHENTICATE_MESSAGE.
![[Pasted image 20250711094303.png]]

- **Algorithm**: The hash is a result of **MD4**(UTF-16-LE(password)).

- Vulnerabilities:
	- *Does not use a salt* (meaning the same passwords will result in the same hash values), making it susceptible to rainbow table attacks.
	  
	- Vulnerable to offline **brute-force attacks**; an 8-character NTLM hash *can be cracked in under 3 hours* with modern GPUs.
	  
	- Susceptible to **Pass-the-Hash** attacks, where an attacker can *use the captured hash to authenticate* without knowing the cleartext password.

- **Structure:** An NTLM hash string typically includes *the username, Relative Identifier (RID), the LM hash, and the NT hash.*
  
- **Example**:
	- Hash: `Rachel:500:aad3c435b514a4eeaad3b935b51304fe:e46b9e548fa0d122de7f59fb6d48eaa2:::`
	- `Rachel` is the username
	- `500` is the Relative Identifier (RID). 500 is the known RID for the `administrator` account
	- `aad3c435b514a4eeaad3b935b51304fe` is the **LM hash** and, if LM hashes are disabled on the system, can not be used for anything
	- `e46b9e548fa0d122de7f59fb6d48eaa2` is the **NT hash**. Can be cracked


## NTLMv1 (Net-NTLMv1)

- **Function:** A network authentication protocol that uses a *challenge-response mechanism* involving both NT and LM hashes.

- **Process:** A server sends an 8-byte random challenge, and the client returns a 24-byte response.

- **Vulnerabilities:** Susceptible to offline cracking and NTLM relay attacks.

- **Limitation:** The captured hashes **cannot** be used for Pass-the-Hash attacks.


#### NTLMv2 (Net-NTLMv2)

- **Improvement:** Introduced in Windows NT 4.0 SP4 and default since Windows Server 2000. It is a more secure alternative to NTLMv1.

- **Enhanced Security:**
	- Hardened against spoofing attacks.
	  
	- Uses a more complex algorithm involving two responses that include HMAC-MD5 hashes of the challenge, user credentials, a client-generated challenge, a timestamp, and the domain name.
	  
	- Significantly more difficult to crack than NTLMv1.

#### Domain Cached Credentials (MSCache2)

- **Purpose:** Allows users to log in to a *domain-joined machine* even when it *cannot* communicate with a Domain Controller (e.g., during a network outage).

- **Mechanism:** The system *saves* the hashes of the last 10 successfully logged-in domain users in the `HKEY_LOCAL_MACHINE\SECURITY\Cache` registry key.

- **Security:**
	- These hashes **cannot** be used for Pass-the-Hash attacks.
	  
	- They are extremely slow and **difficult to crack**, even with powerful hardware. Cracking attempts are often futile unless the password is very weak.
		- Because the passwords are run through the hash function about 10k times

## References:

https://academy.hackthebox.com/module/74/section/1350