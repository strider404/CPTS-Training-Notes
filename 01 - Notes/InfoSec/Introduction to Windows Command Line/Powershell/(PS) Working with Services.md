
2025-04-17 11:06

Tags: #windows #shell #hands-on 

## Working with Services

- [Services](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FWindows%20Fundamentals%2FWindows%20Services%20%26%20Processes) theory see in this link

- **PowerShell Module**: `Microsoft.PowerShell.Management` provides cmdlets for ==service management.==

- `Get-Service`: View services.
	- e.g., `Get-Service | ft DisplayName, Status`
	- Can also use filter
		- `Get-Service | where DisplayName -like '*Defender*'`

- `Start-Service`: Start a service.

- `Stop-Service`: Stop a service.

- `Restart-Service`, `Set-Service`, `Suspend-Service`, etc.

- `Remove-Service` requires PowerShell 7+, otherwise use `sc.exe`.

- Must run Powershell with **Administrator**

- **Remote** computer:
	- `Get-Service -ComputerName <hostname>`
	- `Invoke-Command -ComputerName Host1,Host2 -ScriptBlock { Get-Service -Name 'WinDefend' }`
		- Telling Powershell that we are running this command in a remote computer

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1622)