
2026-05-26 10:48

Tags: #escalation 

## Further Credential Theft

- Administrators and users often rely on built-in Windows features for convenience, leaving credentials exposed in clear text or easily reusable formats.


- **Cmdkey Saved Credentials:** * Users save credentials for tasks like seamless RDP connections.
    - **Enumerate:** `cmdkey /list`
        
    - **Exploit:** Use `runas /savecred /user:<domain>\<user> "COMMAND"` to execute commands as that user without knowing their password.
    - ![[Screenshot_20260526_105742 1.png]]


- **Windows AutoLogon:**
    - Configured for automatic logons on boot; stores credentials in clear text in the registry.
        
    - **Enumerate:** Check the `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon` hive. Look for `DefaultUserName` and `DefaultPassword`.


- **PuTTY Proxy Configurations:**
    - If an administrator configures a PuTTY session to use a proxy, the proxy credentials (sometimes domain admin creds) are stored in clear text.
        
    - **Enumerate:** Query `HKEY_CURRENT_USER\SOFTWARE\SimonTatham\PuTTY\Sessions\<SessionName>` for `ProxyUsername` and `ProxyPassword`.


- **Wi-Fi Passwords:**
    - If the target has a wireless card (e.g., a laptop), you can recover saved Wi-Fi pre-shared keys (PSKs), which can facilitate lateral movement onto corporate wireless networks.
        
    - **Enumerate Profiles:** `netsh wlan show profile`
        
    - **Extract Password:** `netsh wlan show profile <ProfileName> key=clear` (Look under "Key Content").

## Third-Party Applications & Password Managers

- Locally installed applications frequently cache credentials to improve user experience.

- **Browsers (Chrome/Chromium):**
    - Tools like **SharpChrome** can decrypt and dump saved logins and cookies.
        
    - _OpSec Note:_ Extracting these can trigger blue team alerts (e.g., Event IDs 4688 for process creation, or 16385 for DPAPI activity).
    - ![[Screenshot_20260526_105645.png]]


- **Password Managers (KeePass):**
    - KeePass stores passwords locally in a `.kdbx` file.
        
    - **Exploit:** Download the `.kdbx` file, extract the hash using `keepass2john`, and crack it offline using Hashcat (Module `13400`) or John the Ripper. A cracked master password can yield access to entire IT environments.
    - ![[Screenshot_20260526_105714 2.png]]

## Automated Credential Harvesting Tools

- When manual enumeration is too slow or you want to cast a wide net, automated scripts and binaries are highly effective.


- **LaZagne:** * A robust, multi-module tool designed to hunt for credentials across dozens of applications (browsers, chat clients, databases, Git, Wi-Fi, sysadmin tools).
    - **Usage:** Run `lazagne.exe all` to execute all modules and dump discovered cleartext credentials.
    - ![[Screenshot_20260526_111852.png]]


- **SessionGopher:**
    - A PowerShell script specialized in locating and decrypting saved sessions for remote access tools (PuTTY, WinSCP, FileZilla, RDP).
        
    - **Usage:** It queries the `HKEY_USERS` hive (requiring local admin to see all users) and can also search the file system for `.ppk` (private keys) and `.rdp` files.
    - ![[Screenshot_20260526_110219.png]]


- **MailSniper:**
    - If you compromise a domain user with an Exchange inbox, this tool can search their emails for keywords like "password," "creds," or "credentials."



## References:

