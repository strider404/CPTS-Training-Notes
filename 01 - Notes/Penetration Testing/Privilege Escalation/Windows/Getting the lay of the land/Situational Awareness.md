
2026-05-20 17:55

Tags: #escalation  

## Network Information

- Gathering network data helps identify if a host is dual-homed (connected to multiple networks) and reveals potential targets for lateral movement.
	- **View Interface, IP, and DNS Info:** Run `ipconfig /all` to identify current subnets, DNS servers, and whether the host is part of an Active Directory domain.
	    
	- **View the ARP Cache:** Run `arp -a` to reveal *recent communications* with other hosts. This is highly useful for identifying administrators who may be connecting via RDP or WinRM.
		- ![[Screenshot_20260520_175855.png]]
		    
	- **View Routing Tables:** Run `route print` to expose information about the local network architecture and adjacent routable networks.


## Enumerating Protections

- Identifying Anti-Virus (AV), Endpoint Detection and Response (EDR), and application whitelisting solutions is critical before executing enumeration tools or public exploits.
	- **Check Windows Defender Status:** Run `Get-MpComputerStatus` in PowerShell to determine which defensive features are active (pay attention to flags like `RealTimeProtectionEnabled` or `BehaviorMonitorEnabled`).
		- ![[Screenshot_20260520_180021.png]]
		  
		  
	- **List AppLocker Policies:** Run `Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections` to display current application whitelisting rules. This dictates which binaries or scripts a standard user is permitted to execute.
		- ![[Screenshot_20260520_180105.png]]
		  
		  
	- **Test Specific AppLocker Restrictions:** Run `Get-AppLockerPolicy -Local | Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone` to explicitly validate whether a specific executable (like `cmd.exe` or `powershell.exe`) is allowed or denied for your current user context.
		- ![[Screenshot_20260520_180123.png]]
## References:

https://academy.hackthebox.com/app/module/67/section/927