
2026-08-12 15:39

Tags: 

## BoardLight

- Nmap
	- ![](Pasted%20image%2020260812154005.png)
	- Port 22, 80
	- Website:
	- ![](Pasted%20image%2020260812154058.png)
	- Vhost enumeration
	- ![](Pasted%20image%2020260812154337.png)
	- Dolibarr 17.0.0 is running on this vhost
	- ![](Pasted%20image%2020260812154355.png)
	- Can be logged in with admin:admin
	- ![](Pasted%20image%2020260812154509.png)

- Exploit
	- This version is vulnerable to CVE-2023-30253
	- Authenticated attackers can bypass input validation mechanisms in PHP tag filtering by using uppercase PHP tags (`<? PHP` instead of `<? php`), allowing them to inject and execute arbitrary PHP code on the server.
	- Download and use the POC for the rev shell
	- ![](Pasted%20image%2020260812160207.png)
	- ![](Pasted%20image%2020260812160216.png)
	- Find the Dolibarr database connection information in the `/html/crm.board.htb/htdocs/conf/conf.php` file
	- ![](Pasted%20image%2020260812162207.png)
	- dolibarrowner:serverfun2$2023!!
	- Use that credential to query MySQL db
	- ![](Pasted%20image%2020260812162440.png)
	- Nothing useful in these
	- Check `/etc/passwd` for the users that have default shell
	- ![](Pasted%20image%2020260812163322.png)
	- We have root and larissa
	- She reuses the password serverfun2$2023!!
	- ![](Pasted%20image%2020260812163427.png)


- Escalation
	- sudo -l  and id nothing
	- Run linpeas
	- ![](Pasted%20image%2020260812171030.png)
	- Find enlightenment_sys has SUID set
	- ![](Pasted%20image%2020260812171344.png)
	- It is using 0.23.1 => Vulnerable to CVE-2022-37706
	- Download the POC and nuke
	- ![](Pasted%20image%2020260812171719.png)
## References:

