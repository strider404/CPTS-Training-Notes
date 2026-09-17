
2026-05-19 18:40

Tags: #escalation  

## Dirty Pipe

- **Dirty Pipe** is a critical vulnerability within the Linux kernel's **pipe mechanism** that allows local, unprivileged users to overwrite data in arbitrary read-only files (including root-owned files), provided they have basic read access to them.

## Vulnerability Profile

|**Attribute**|**Detail**|
|---|---|
|**CVE Reference**|CVE-2022-0847 (similar concept to 2016's Dirty COW)|
|**Scope**|Linux Kernel versions **5.8 to 5.17** (includes vulnerable Android devices)|
|**Prerequisite**|Read permission on the target file or access to a local SUID binary|

## The Two Exploitation Paths

- Public Proof-of-Concept (PoC) scripts typically provide two distinct methods to achieve an immediate root shell:

- **Path 1: Target File Manipulation** (`exploit-1`)
	- **Target:** Sensitive configuration files like `/etc/passwd`.
	    
	- **Mechanism:** The exploit injects data directly into the file's page cache. It backs up `/etc/passwd`, modifies the root user's password field to a known value (like `"piped"`), spawns a root shell, and then cleanly restores the original file to minimize detection.

- **Path 2: SUID Binary Hijacking** (`exploit-2`)
	- **Target:** System binaries configured with the SUID bit set (e.g., `/usr/bin/sudo`, `/usr/bin/su`, `/usr/bin/pkexec`).
	    
	- **Mechanism:**
	    1. The attacker locates vulnerable binaries using:
	        1. `find / -perm -4000 2>/dev/null`
	           
	    2. The exploit targets the chosen binary's page cache, temporarily injecting malicious shellcode into it.
	       
	    3. When the binary is executed, it runs the injected code with full root permissions, granting the attacker a root shell before restoring the original binary on disk.




## References:

