
2026-05-11 10:49

Tags: #linux #escalation

## Introduction

- **Core Objective:** Escalate from a low-privileged shell to the `root` account to gain full administrative control, access sensitive files, capture traffic, or pivot into Active Directory.

- **Primary Methodology:** Thorough enumeration (manual or via scripts like LinEnum) to uncover system misconfigurations and vulnerabilities.

- **Key Enumeration Targets:**
    - **OS and Kernel Versions:** Identify the specific distribution and kernel to find matching public exploits. _(Note: Kernel exploits carry a risk of crashing the system)._
        
    - **Running Services and Installed Packages:** Hunt for outdated or inherently vulnerable software running with root privileges (e.g., specific versions of Nagios, Screen, Exim)
        
    - **User Activity:** Monitor logged-in users and terminal-attached processes to find avenues for lateral movement
        
    - **Home Directories:** Inspect accessible user folders for exposed SSH private keys, sensitive `.config` files, and `.bash_history` (which often leaks cleartext passwords or workflows).
        
    - **Sudo Privileges:** Use `sudo -l` to identify commands the current user can execute as root, prioritizing entries with the `NOPASSWD` tag.
        
    - **Configuration Files:** Search `.conf` and `.config` files system-wide for hardcoded credentials or secrets.
        
    - **Password Hashes:** Check for read access to `/etc/shadow` or hashes improperly stored in `/etc/passwd` to perform offline brute-force cracking.
        
    - **Cron Jobs:** Review scheduled tasks for exploitable flaws, such as weak file permissions or the use of relative paths in scripts executed by root.
        
    - **Additional Drives:** Look for unmounted file systems (`lsblk`) that might house unprotected backups or sensitive data.
        
    - **Special Permissions (SETUID/SETGID):** Search for binaries flagged with these permissions, as they allow users to execute the file with the privileges of the file owner (often root).
        
    - **Writable Locations:** Identify world-writable directories (useful for dropping exploit payloads) and writable files (allowing modification of scripts that root regularly executes).



## References:

https://academy.hackthebox.com/app/module/51/section/466