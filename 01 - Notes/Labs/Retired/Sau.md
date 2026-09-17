
2026-07-29 17:48

Tags: 

## Sau

- Nmap
	- ![[Pasted image 20260729174907.png]]
	- Port 22, 80, 55555

- In port 55555, it is using request-basket 1.2.1
	- ![[Pasted image 20260729184331.png]]
	- It has a CSRF vulnerability CVE-2023-27163
	- Craft a payload to create a basket that forward our requests to port 80
	- ![[Pasted image 20260729184456.png]]

- Get to `http://10.129.35.185:55555/lol`
	- ![[Pasted image 20260729184534.png]]
	- It is using Mailtrail 0.53
	- It has a Unauthenticated Command Injection vulnerability
	- Exploit it with msfconsole
	- ![[Pasted image 20260729184805.png]]
	- Get the shell & user flag
	- ![[Pasted image 20260729184826.png]]

- This user can run systemctl status with root
	- ![[Pasted image 20260729184859.png]]
	- Using version systemd 245 (245.4-4ubuntu3.22)
	- Vulnerable to CVE-2023-26604

- Exploit
	- ![[Pasted image 20260729185013.png]]
	- Need to use smaller terminal to make it works

## References:

