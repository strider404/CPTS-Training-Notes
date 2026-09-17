
2026-07-30 15:49

Tags: 

## Devvortex

- Nmap
	- ![[Pasted image 20260730154931.png]]
	- Port 22, 80

- Subdomain fuzzing
	- ![[Pasted image 20260730160303.png]]
	- dev.devvortex.htb
	- Directory fuzzing
	- ![[Pasted image 20260730160337.png]]
	- ![[Pasted image 20260730160351.png]]
	- Administrator page
	- Check the version by going to the /administrator/manifests/files/joomla.xml endpoint
	- ![[Pasted image 20260730160744.png]]
	- Version 4.2.6

- It is vulnerable to CVE-2023-23752
	- Clone a POC
	- ![[Pasted image 20260730161310.png]]
	- ![[Pasted image 20260730162055.png]]
	- lewis:P4ntherg0t1n5r3c0n##


- Use that to login to Joomla
	- Go to Template
	- ![[Pasted image 20260805172511.png]]
	- Spot a php template
	- Change the error.php to a reverse shell
	- ![[Pasted image 20260805172537.png]]
	- Trigger it with curl
	- ![[Pasted image 20260805172553.png]]
	- ![[Pasted image 20260805172619.png]]
	- Login to mysql
	- ![[Pasted image 20260805172646.png]]
	- ![[Pasted image 20260805172702.png]]
	- ![[Pasted image 20260805172714.png]]
	- `$2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy/yBtkIj12`
	- logan:tequieromucho

- SSH to him
	- ![[Pasted image 20260805172859.png]]
	- sudo -l
	- ![[Pasted image 20260805172953.png]]
	- Can run /usr/bin/apport-cli with sudo

- It is vulnerable to **CVE-2023-1326**
	- **Privilege Inheritance:** When `apport-cli` is invoked via `sudo` or elevated execution primitives, the entire process—including any spawned subprocesses like the pager—inherits root privileges.
    
	- **Pager Execution:** Instead of executing the display pager with the real calling user's permissions, `apport-cli` invokes the pager as `root`.
    
	- **Pager Shell Escape:** Default interactive pagers such as `less` feature shell escape syntax (e.g., typing `!/bin/bash` or `!sh` inside the pager). Because the pager itself is running as `root`, escaping to a shell yields an interactive root prompt.

- Escalation
- Update terminal size
	- stty rows 5 cols 80
	- ![[Pasted image 20260805174154.png]]
	- Create a crash file
	- `sleep 100 & kill -SEGV %1`
	- Run: `sudo /usr/bin/apport-cli -c /var/crash/_usr_bin_sleep.1000.crash`
	- Select V view report
	- Escape it with !/bin/bash
## References:

