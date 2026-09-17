
2026-05-11 15:54

Tags: #escalation  

## Credential Hunting

- **Objective:** *Locate credentials* to escalate privileges (to other users or root), access databases, or pivot to other systems.


- **Common File Types:** Search within configuration files (`.conf`, `.config`, `.xml`), shell scripts, backup files (`.bak`), and plain text files.


- **Key Locations:**
    - **User Activity:** Check the `.bash_history` file for passwords passed as command arguments.
        
    - **Web Root (`/var`):** Frequently contains hardcoded credentials, such as MySQL connection strings in WordPress `wp-config.php` files.
        
    - **Mail/Spool Directories:** Often accessible and may store sensitive communications or system data.


- **Enumeration Command:** Use `find` to hunt for configuration files across the file system while excluding noisy directories like `/proc`: `find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null`
	- ![[Pasted image 20260511155826.png]]

## SSH Keys

- **Objective:** Discover accessible SSH private keys (e.g., `id_rsa`) to gain unauthorized access.
    
- **Privilege Escalation:** Locating a private key belonging to a higher-privileged user allows you to reconnect to the current machine with elevated rights.
    
- **Lateral Movement:** Private keys can also be used to authenticate into entirely different servers within the environment.
    
- **Target Identification (`known_hosts`):** Always inspect the `~/.ssh/known_hosts` file alongside private keys. This file lists the public keys and IPs/hostnames of systems the user has previously connected to, providing a direct map for lateral movement.

- ![[Pasted image 20260511155939.png]]


## References:

