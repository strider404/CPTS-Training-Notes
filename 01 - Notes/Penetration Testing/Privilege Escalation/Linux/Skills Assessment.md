
2026-05-20 08:48

Tags:  #escalation 

## Skills Assessment


- ![[Pasted image 20260520084933.png]]
- No sudo => permission based: No
- No sus group
- Linux 5.4.0-45 - Ubuntu 2020

- Bash history
	- ![[Pasted image 20260520103433.png]]
	- But nothing there


- Run LinPeass
	- ![[Pasted image 20260520103329.png]]
	- ![[Pasted image 20260520103341.png]]
	- ![[Pasted image 20260520103118.png]]
	- ![[Pasted image 20260520103145.png]]
	- ![[Pasted image 20260520103205.png]]

- Look for htb-student hidden files
	- ![[Pasted image 20260520110654.png]]
	- `find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null | grep htb-student`


- Look for another users:
	- ![[Pasted image 20260520110934.png]]
	- Search barry's history
	- ![[Pasted image 20260520110959.png]]
	- `sshpass -p 'i_l0ve_s3cur1ty!' ssh barry@10.129.235.16`
	- ![[Pasted image 20260520112042.png]]
	- ssh to him, get the flag
	- Running mysql as root, and tmux
		- ![[Pasted image 20260520112254.png]]
	- ![[Pasted image 20260520113206.png]]
	- He is in adm group => read the /var/log
	- ![[Pasted image 20260520144943.png]]
	- flag 3 obtained

- Run linpeass again, there is a tomcat backup file with barry
	- ![[Pasted image 20260520162025.png]]
	- ![[Pasted image 20260520162044.png]]
	- credential: username="tomcatadm" password="T0mc@t_s3cret_p@ss!"
	- ![[Pasted image 20260520163250.png]]
	- make a `.war` file the upload it
	- ![[Pasted image 20260520163322.png]]
	- get the shell and the flag


- Get an interactive shell TTY with `python3 -c 'import pty; pty.spawn("/bin/sh")'` (Required)

- This user can execute busctl with root
	- ![[Pasted image 20260520165329.png]]

- Check gtfobin and run command
	- `sudo busctl --show-machine`
	- `!/bin/sh`


- Dropped in root shell
	- ![[Pasted image 20260520165433.png]]


## References:

