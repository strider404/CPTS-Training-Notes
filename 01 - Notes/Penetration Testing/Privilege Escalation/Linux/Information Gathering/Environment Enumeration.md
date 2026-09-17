
2026-05-11 14:14

Tags: #escalation  

## Environment Enumeration

- The goal is to **identify OS details, running services, and misconfigurations to locate potential easy wins or public exploits.**

## Initial Situational Awareness

- **whoami:** Identifies the current user context.
    
- **id:** Reveals the user's assigned groups and associated privileges.
    
- **hostname:** Discloses the server name, which may hint at its role or naming conventions.
    
- **ifconfig / ip a:** Displays the current subnet and any additional network interfaces.
    
- **sudo -l:** Lists commands the user can execute as root without a password for immediate privilege escalation.
    

## System and OS Enumeration

- **OS Version:** `cat /etc/os-release` identifies the Linux distribution and release cycle to spot outdated systems.
	- ![[Pasted image 20260511142331.png]]
	  
- **Kernel Version:** `uname -a` or `cat /proc/version` checks for specific vulnerable kernels (use kernel exploits cautiously as they can crash systems).
	- ![[Pasted image 20260511142406.png]]
	  
- **CPU Architecture:** `lscpu` reveals processor details and whether the system is 32-bit or 64-bit.
	- ![[Pasted image 20260511142417.png]]
	  
- **Environment Variables:** `env` outputs active variables that might contain sensitive data like passwords.
	- ![[Pasted image 20260511142435.png]]
	  
- **PATH Variable:** `echo $PATH` shows executable search paths, which can be exploited if misconfigured.
	- ![[Pasted image 20260511142506.png]]
	  
- **Login Shells:** `cat /etc/shells` lists available shells (e.g., bash, tmux, screen) to check for outdated versions like Bash 4.1 (Shellshock).
	- ![[Pasted image 20260511142516.png]]


## Network and Device Enumeration

- **Block Devices:** `lsblk` lists hard disks, USBs, and optical drives to find unmounted file systems.
	- ![[Pasted image 20260511142541.png]]
	    
- **Mounted Drives:** `df -h` and `cat /etc/fstab` show mounted file systems that may contain credentials or sensitive backups.
	- ![[Pasted image 20260511142557.png]]
	    
- **Printers:** `lpstat` checks for attached printers and queued jobs.
    
- **Routing Table:** `route` or `netstat -rn` reveals internal network routes and adjacent subnets.
	- ![[Pasted image 20260511142628.png]]
	    
- **ARP Cache:** `arp -a` displays recently communicated hosts, useful for planning lateral movement.
	- ![[Pasted image 20260511142646.png]]
	    
- **DNS:** `/etc/resolv.conf` can expose internal Active Directory environments.


## User and Group Enumeration

- **All Users:** `cat /etc/passwd` lists system users, their IDs, home directories, and default shells.
	- ![[Pasted image 20260511142718.png]]
	    
- **Hashes:** Occasionally found directly in `/etc/passwd`; identifiable by their prefix (e.g., `$1$` for MD5, `$5$` for SHA-256, `$6$` for SHA-512).
	- ![[Pasted image 20260511142752.png]]
	    
- **Active Shells:** `grep "sh$" /etc/passwd` filters for users capable of logging into the system.
	- ![[Pasted image 20260511142804.png]]
	    
- **Groups:** `cat /etc/group` displays all system groups and their members.
	- ![[Pasted image 20260511142814.png]]
	    
- **Specific Group Info:** `getent group <name>` lists the members of a targeted group, such as `sudo`.
	- ![[Pasted image 20260511142826.png]]
	    
- **Home Directories:** `ls /home` maps out user folders to search for `.bash_history`, SSH keys, and config files.
	- ![[Pasted image 20260511142834.png]]

## Files, Folders, and Defenses

- **Hidden Files:** `find / -type f -name ".*"` locates hidden files containing notes, configurations, or command history.
	- ![[Pasted image 20260511142902.png]]
	    
- **Hidden Directories:** `find / -type d -name ".*"` reveals hidden folders like `.ssh`, `.gnupg`, or `.config`.
    
- **Temporary Folders:** `/tmp` (cleared on reboot/10 days), `/var/tmp` (kept up to 30 days), and `/dev/shm` often hold script outputs, logs, or temporary sensitive data.
    
- **System Defenses:** Note the presence of protections like Exec Shield, iptables, AppArmor, SELinux, Fail2ban, Snort, or ufw to tailor your attack and avoid wasting time.
## References:

https://academy.hackthebox.com/app/module/51/section/1592