
2026-05-26 09:59

Tags: #escalation 

## Network Shares & Loose Permissions

- In **Active Directory** environments, it is common to find network file shares (e.g., user-specific folders) with overly permissive access rights (like "Domain Users" having read access). These are prime targets for sensitive data.


- **What to look for:**
	- **Virtual Drives & Keys:** `.vmdk`, `.vdhx`, `.ppk` (SSH keys).
	    
	- **Password Databases:** `.kdbx` (KeePass).
	    
	- **Careless Storage:** Passwords stored in Excel/Word documents, OneNote, or standard `passwords.txt` files.
	    
	- **Automation:** Tools like **Snaffler** can be used to efficiently crawl network shares for these specific extensions.

## Manual File & String Enumeration

| **Objective**              | **CMD Command Examples**                 | **PowerShell Command Examples**                        |
| -------------------------- | ---------------------------------------- | ------------------------------------------------------ |
| **Search File Contents**   | `findstr /si password *.xml *.ini *.txt` | `Select-String -Path C:\path\*.txt -Pattern password`  |
| **Search File Extensions** | `dir /S /B *pass*.txt == *.config`       | `Get-ChildItem C:\ -Recurse -Include *.config, *.cred` |
| **Locate Specific Files**  | `where /R C:\ *.config`                  | (Use `Get-ChildItem` as above)                         |

- **Note on `findstr` flags:** > * `/S` searches the current directory and all subdirectories.
	- `/I` makes the search case-insensitive.
	    
	- `/M` prints only the filename if a match is found.
	    
	- `/P` skips files with non-printable characters.
	    
	- `/N` prints the line number before each matching line.
## The Sticky Notes Goldmine

- Users frequently **paste passwords into Windows Sticky Notes**, unaware that the data is saved in a local SQLite database.
  
  
- **File Location:** `C:\Users\<user>\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqlite`


- **Associated Files:** You will often see `plum.sqlite`, `plum.sqlite-shm`, and `plum.sqlite-wal`.
    

- **Methods to Extract Data:**
	1. **Offline SQLite Browser:** Download the `plum.sqlite` files to your attack box and open them in a tool like [DB Browser for SQLite](https://sqlitebrowser.org/dl/). Use the query: `SELECT Text FROM Note;`
		1. ![[Pasted image 20260526100620.png]]
		    
	2. **PowerShell (PSSQLite):** Import the [`PSSQLite`](https://github.com/RamblingCookieMonster/PSSQLite) module on the target machine and query the database directly using `Invoke-SqliteQuery`.
		1. ![[Pasted image 20260526100721.png]]
		    
	3. **Linux `strings`:** Download the database files to your attack box and run `strings plum.sqlite-wal` to parse through the raw text (less efficient, but works in a pinch).



## Other High-Value Target Files

- Keep an eye out for standard system, configuration, and log files that routinely leak administrative credentials or sensitive system states.

- **Key directories and files include:**
	- **SAM/System Backups:** `%WINDIR%\repair\sam`, `%WINDIR%\repair\system`
	    
	- **Config Files:** `%WINDIR%\system32\config\*.sav`, `C:\ProgramData\Configs\*`
	    
	- **Web & Network Logs:** `%WINDIR%\iis6.log`, `%WINDIR%\debug\NetSetup.log`
	    
	- **User Data:** `%USERPROFILE%\ntuser.dat`, `index.dat` in IE temp folders.
	    
	- **PowerShell Scripts:** `C:\Program Files\Windows PowerShell\*`
	    
	- **Memory Paging:** `%SYSTEMDRIVE%\pagefile.sys`
## References:

https://academy.hackthebox.com/app/module/67/section/639