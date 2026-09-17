
2025-04-18 17:37

Tags: #windows #shell  #hands-on

## Windows Event Log

- **Event:** Any identifiable action or occurrence within the system (e.g., user interaction, application crash, login attempt).

- **Event Logging:** A standardized service in Windows that ==records events== from various sources (hardware, OS, applications) into structured logs.

- **Event Log Categories**:
	- **System:** OS-related events (e.g., service startup failures).
	- **Security:** Authentication and access-related events (e.g., login attempts).
	- **Application:** Logs from user-installed applications.
	- **Setup:** OS and Active Directory installation events.
	- **Forwarded Events:** Logs from other networked systems.

- **Event Types**:
	- **Error:** Critical system/application failures.
	- **Warning:** Potential issues (e.g., low disk space).
	- **Information:** Successful operations (e.g., service started).
	- **Success Audit / Failure Audit:** Results of security access checks.

- **Severity Levels:**
	- **Verbose (5)** to **Critical (1)**, indicating increasing importance and urgency.

- **Event Log Structure**:
	- Log name, timestamp, category, Event ID
	- Source (originating app or component)
	- Severity level, user, and host machine name

- The EventLog service (**svchost.exe**) manages logging and starts automatically with the system.

- **Log Storage**: stored in `.evtx` format in `C:\Windows\System32\winevt\logs`.

- **Accessing Logs**:
	- **Graphical Interface:** Event Viewer
	- **Command-Line Tools:**
	    - `wevtutil` (CLI utility)
	    - `Get-WinEvent` (PowerShell cmdlet)


## Interacting with the Windows Event Log

- `wevtutil`: 
	- `el`: List all available logs.
	- `gl <log>`: Display config info (enabled status, size, permissions).
		- `wevtutil gl "Windows PowerShell`"
	- `gli <log>`: Get status details (creation time, file size, record count).
		- `wevtutil gli "Windows PowerShell"`
	- `qe <log>`: Query logs (e.g., show latest events).
		- `wevtutil qe Security /c:5 /rd:true /f:text`
	- `epl <log> <file>`: Export logs for offline analysis.
		- `wevtutil epl System C:\system_export.evtx`

- `Get-WinEvent`: More scriptable and versatile than `wevtutil` -> better in automation, deeper filtering
	- `-ListLog *`: List all logs and record counts.
	- `-LogName <name> -MaxEvents <n>`: Get last n events
	- `-Oldest`: Fetch from oldest to newest.
	- `-FilterHashtable`: Filter by log, event ID, or severity level.
		- `Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625 '}`
		- Can use Select-Object to elaborate
			- `Get-WinEvent -FilterHashTable @{LogName='System';Level='1'} | select-object -ExpandProperty Message`
		- [Creating Get-WinEvent queries with FilterHashtable - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/scripting/samples/creating-get-winevent-queries-with-filterhashtable?view=powershell-7.5)
## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1615)
