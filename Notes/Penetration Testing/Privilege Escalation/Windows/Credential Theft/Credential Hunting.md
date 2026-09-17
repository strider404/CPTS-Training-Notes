
2026-05-25 10:46

Tags: #escalation 

## Credential Hunting

- Finding **exposed credentials** during privilege escalation enumeration can immediately grant local administrative access, provide an initial foothold into an Active Directory domain, or allow for lateral movement. Applications and users frequently leave credentials in predictable, accessible locations across a Windows system.

## Application Configuration Files

- Software developers and system administrators often ignore best practices and store passwords in cleartext within configuration files. If you land on a system as an unprivileged user, searching these files can reveal credentials for highly privileged accounts.


- **Target Files:** `.txt`, `.ini`, `.cfg`, `.config`, `.xml` (e.g., IIS `web.config` files found in `C:\inetpub\wwwroot\`).


- **The Hunt:** Use the native `findstr` utility to recursively search for the string "password" inside specific extensions:
	- `findstr /SI /C:"password" *.txt *.ini *.cfg *.config *.xml`


## Browser Dictionary Files

- When users type sensitive information (like custom passwords) into an email client or browser-based application, the built-in spellchecker flags the word with a red underline. To get rid of the distraction, users often click **"Add to dictionary"**, unintentionally caching their password in plaintext.


- **Target File (Chrome):** `C:\Users\<USERNAME>\AppData\Local\Google\Chrome\User Data\Default\Custom Dictionary.txt`


- **The Hunt:** Inspect the custom dictionary file for unique strings:
	- `gc 'C:\Users\htb-student\AppData\Local\Google\Chrome\User Data\Default\Custom Dictionary.txt' | Select-String password`


## Unattended Installation Files

- When Windows is deployed automatically via images, configuration settings are passed via answer files. These files frequently define automated logon credentials or create local administrative accounts, storing passwords in either cleartext or easily reversible Base64 encoding.


- **Target File:** `unattend.xml` (or variations left behind in development or backup folders by sysadmins).


- **Key XML Element to Look For:**
	- <`AutoLogon>`
	    `<Password><Value>local_4dmin_p@ss</Value><PlainText>true</PlainText></Password>`
	    `<Username>Administrator</Username>`
	`</AutoLogon>`


## PowerShell History Files

- Starting with PowerShell 5.0, the `PSReadLine` module automatically logs command history to a plaintext file. Administrators frequently pass raw credentials over the command line when executing remote management commands (such as using `wevtutil` with the `/u` and `/p` flags).


- **Default Path:** `C:\Users\<username>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`


- **To Find the Current Save Path:**
	- `(Get-PSReadLineOption).HistorySavePath`

- **To Read the Current User's History:**
	- `gc (Get-PSReadLineOption).HistorySavePath`

- **Multi-User Mass Dump (Post-Exploitation One-Liner):** If you compromise a system or eventually elevate to local admin, run this loop to scrape the PowerShell history files of _all_ users on the system:
	- `foreach($user in ((ls C:\users).fullname)){cat "$user\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt" -ErrorAction SilentlyContinue}`

## Saved PowerShell Credentials (`Export-Clixml`)

- Sysadmins often automate tasks by exporting credential objects to a file using `Export-Clixml`. While these files encrypt the password using the Windows Data Protection API (DPAPI), they are bound to the user account that created them.


- **The Vulnerability:** If you have gained execution control within the context of that specific user (or can successfully abuse DPAPI), you can import the XML file and trick PowerShell into decrypting it for you on the spot.


- **The Recovery Process:**
	- ![[Pasted image 20260525105415.png]]
## References:

