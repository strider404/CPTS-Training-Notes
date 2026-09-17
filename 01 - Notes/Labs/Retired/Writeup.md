
2026-08-13 19:41

Tags: 

## Writeup

- Nmap
	- ![](Pasted%20image%2020260813194111.png)
	- Port 22,80
	- robots.txt: /writeup/
	- The page
	- ![](Pasted%20image%2020260813194505.png)
	- ![](Pasted%20image%2020260813194520.png)
	- Using CMS Made Simple
	- Through some search, it might be vulnerable to SQL injection
	- Using searchsploit
	- ![](Pasted%20image%2020260813201629.png)
	- Try the CVE-2019-9059
	- Because it is python2 so i need to download extra library
	- ![](Pasted%20image%2020260813204133.png)
	- Found it
	- Create a hash file and crack it with hashcat
	- 62def4866937f08cc13bab43bb14e6f7:5a599ef579066807
	- Mode 20 (md5)
	- ![](Pasted%20image%2020260813204239.png)
	- jkr:raykayjay9
	- Connect through ssh and get the flag

- **Escalation**
	- sudo -l is not available
	- ![](Pasted%20image%2020260813204603.png)
	- id check
	- ![](Pasted%20image%2020260813204625.png)
	- `staff` group is dangerous
	- So i ran linpeas
	- ![](Pasted%20image%2020260813205044.png)
	- If a root process, cron job, or service executes a command or script that calls a binary without specifying an absolute path—or if the $PATH configuration prioritizes `/usr/local/bin` or `/usr/local/sbin` over `/bin` or `/usr/bin`—a user in the `staff` group could create a malicious, counterfeit binary or script in `/usr/local/bin` and wait for root to execute it.
	- Some sus cron jobs
	- ![](Pasted%20image%2020260813205427.png)
	- Download pspy - a command line tool designed to **snoop on processes without need for root permissions**, allows you to see commands run by other users, **cron jobs,** etc. as they execute.
	- Upload it through scp
	- As we login through ssh
	- ![](Pasted%20image%2020260818171727.png)
	- /etc/update-motd.d/10-uname triggered when logging in 
	- sh -c /usr/bin/env -i PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin run-parts --lsbsysinit /etc/update-motd.d > /run/motd.dynamic.new
	- /run/motd.dynamic.new was called, PATH was specified before calling the **run-parts** binary 
	- Create a malicious run-parts binary in /usr/local/bin
	- ![](Pasted%20image%2020260818172541.png)
	- Which allow SUID in /bin/bash binary
	- Give it execution with chmod +x /usr/local/bin/run-parts
	- Login
	- ![](Pasted%20image%2020260818173236.png)
	- Success 
	- ![](Pasted%20image%2020260818173305.png)


## References:

