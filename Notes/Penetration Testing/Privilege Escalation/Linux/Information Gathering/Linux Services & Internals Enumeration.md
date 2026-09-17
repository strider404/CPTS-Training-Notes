
2026-05-11 15:28

Tags: #escalation  

## Linux Services & Internals Enumeration

- The goal of this phase is to analyze the **internal configurations, running services, and integrated processes** of the host to uncover pathways for privilege escalation.

## Network & Communication

- **Network Interfaces:** Use `ip a` or `ifconfig` to identify current IP addresses and uncover additional subnets for potential pivoting.
	- ![[Pasted image 20260511153952.png]]


- **Hosts File:** Check `cat /etc/hosts` for hardcoded internal network IPs, DNS names, and routing targets.
	- ![[Pasted image 20260511154021.png]]


## User Activity & Tracking

- **Login History:** Run `lastlog` to see user login habits, which helps identify frequently used accounts versus neglected ones.
	- ![[Pasted image 20260511154106.png]]


- **Active Sessions:** Use `w`, `who`, or `finger` to see if other users or administrators are currently sharing the system.
	- ![[Pasted image 20260511154120.png]]


- **Command History:** Review the `history` command or locate hidden history files (`find / -type f \( -name *_hist -o -name *_history \)`) to find exposed passwords, git interactions, or administrative commands.
	- ![[Pasted image 20260511154140.png]]

## Scheduled Tasks & System Data

- **Cron Jobs:** Inspect directories like `/etc/cron.daily/` for scheduled tasks. Weak permissions or relative paths in these scripts allow for easy hijacking.
	- ![[Pasted image 20260511154355.png]]


- **Proc Filesystem (`/proc`):** Leverage this virtual filesystem to extract live data about hardware, memory allocation, and running processes (e.g., reading command-line arguments via `find /proc -name cmdline`).
	- ![[Pasted image 20260511154409.png]]

## Software, Packages & Binaries

- **Installed Packages:** Generate a list of installed software (e.g., `apt list --installed`) to search for outdated or vulnerable applications.
	- ![[Pasted image 20260511154733.png]]


- **Sudo Version:** Execute `sudo -V` to check for legacy vulnerabilities within the sudo application itself.
	- ![[Pasted image 20260511154740.png]]


- **System Binaries:** Enumerate binaries in `/bin`, `/usr/bin/`, and `/usr/sbin/`.
	- ![[Pasted image 20260511154757.png]]


- **GTFOBins Exploitation:** Cross-reference installed binaries with the [GTFOBins](https://gtfobins.org/) database to identify native tools that can be abused to spawn elevated shells.
	- ![[Pasted image 20260511154811.png]]



- **System Call Tracing:** Use `strace` (e.g., `strace ping...`) to track exactly how a program interacts with the OS, which can reveal hidden file paths, misconfigurations, or sensitive data requests.
	- ![[Pasted image 20260511155030.png]]


## Files & Processes

- **Configuration Files:** Search for `.conf` and `.config` files. Even if a directory is restricted, globally readable configs often leak credentials, keys, or internal routing logic.
	- ![[Pasted image 20260511155101.png]]
	  

- **Custom Scripts:** Hunt for `.sh` files. Custom admin scripts are frequently poorly secured and can be exploited or analyzed to understand internal workflows.
	- ![[Pasted image 20260511155111.png]]
	  
- **Running Services:** Use `ps aux | grep root` to identify exactly which scripts, tools, and services are currently executing with root privileges.
	- ![[Pasted image 20260511155121.png]]
## References:

