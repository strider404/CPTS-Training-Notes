
2026-05-12 21:49

Tags: #escalation  

## Setuid (Set User ID)

- **Concept:** A special file permission that *allows a user to run an executable with the permissions of the file's owner* (typically `root`), granting temporary elevated privileges.


- **Identification:** Denoted by an `s` in the owner's permission bits (e.g., `-rwsr-xr-x`).


- **Enumeration Command:** `find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null`
	- ![[Pasted image 20260512215212.png]]


- **Exploitation:** Attackers can escalate privileges by reverse-engineering these binaries to find vulnerabilities, or by abusing the intended features of the program to execute unauthorized commands.


## Setgid (Set Group ID)

- **Concept:** Functions identically to setuid, but *grants* the executing user the permissions of the file's _group_ rather than the owner.


- **Enumeration Command:** `find / -uid 0 -perm -6000 -type f 2>/dev/null`
	- ![[Pasted image 20260512215308.png]]


- **Exploitation:** Abused in the exact same manner as setuid binaries to move laterally or escalate privileges.

## GTFOBins

- **Concept:** A curated *repository* of legitimate, standard Unix binaries and scripts that can be exploited to bypass security restrictions.
	- [Link](https://gtfobins.org/)


- **Attack Vectors:** These binaries can be abused to:
    - Break out of restricted shells.
        
    - Escalate privileges (e.g., abusing `sudo` rights).
        
    - Spawn reverse shell connections.
        
    - Read, write, or transfer files.


- **Practical Example (`apt-get`):** If a user has `sudo` privileges for `apt-get`, they can inject a shell command into the update process to gain a root shell:
    - `sudo apt-get update -o APT::Update::Pre-Invoke::=/bin/sh`
    - ![[Pasted image 20260512215401.png]]


- **Attacker Strategy:** Recognizing standard binaries listed on GTFOBins is a critical skill for quickly identifying misconfigurations and finding escalation paths once initial access is achieved.

## References:

