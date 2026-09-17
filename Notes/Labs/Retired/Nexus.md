
2026-07-24 09:32

Tags: 

## Nexus

- Nmap scan:
	- ![[Pasted image 20260724093228.png]]
	- Port 22, 80

- whatweb
	- ![[Pasted image 20260724095957.png]]

- There is an email here
	- ![[Pasted image 20260724101739.png]]

- Subdomain Fuzzing
	- ![[Pasted image 20260724100546.png]]
	- git.nexus.htb
	- ![[Pasted image 20260724100640.png]]
	- Found a repo in Explore tab
	- ![[Pasted image 20260724100747.png]]
	- We have the password from the last commit
		- ![[Pasted image 20260724101443.png]]
	- Visit billing.nexus.htb
		- ![[Pasted image 20260724101513.png]]
		- Try the email and the password found
		- ![[Pasted image 20260724101823.png]]
		- ![[Pasted image 20260724101836.png]]



- It is vulnerable to **CVE-2026-38526**

- Upload a PHP reverse shell from the compose email part:
	- ![[Pasted image 20260724105422.png]]
	- ![[Pasted image 20260724105437.png]]
	- Catch the reponse with burp suite and get the URL
	- ![[Pasted image 20260724105508.png]]
	- Start nc, go to that URL to trigger the rev shell
	- ![[Pasted image 20260724105547.png]]
	- Go to the home directory of this user and get another .env file
	- ![[Pasted image 20260724105624.png]]
	- Get the DB username & password
	- ![[Pasted image 20260724105653.png]]
	- y27xb3ha!!74GbR

- Query the DB and get credential for another user
	- ![[Pasted image 20260724105716.png]]
	- Hash: `$2y$10$ez0AouNyeP4NmwjLSV5vCOAJxMLi.6fCKmGC3M6Ve5xJmWJOLRJ5i`
	- Nah. just use the cleartext
	- ![[Pasted image 20260724145327.png]]
## References:

