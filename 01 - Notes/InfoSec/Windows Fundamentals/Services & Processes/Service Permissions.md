
2025-03-21 09:30

Tags: #windows  

## Service Permissions

- Services can be misconfigured -> can be exploited

## Examining Services using services.msc

![[Pasted image 20250321094030.png]]

- If the NTFS permissions of the directory are weak -> executable can be replaced with a malware

![[Pasted image 20250321094214.png]]

- Local System privileges (highest privileges an invidual can have) set by default -> can be exploited 

## Examining services using sc

- `sc.exe qc`: query the service (sc qc Service_name)
	- Can query a service from remote device (`sc.exe //hostname or ip of box query ServiceName`)
	- Start/stop services: `sc.exe stop wuauserv`
	- Change services' exe path: `sc.exe config wuauserv binPath=C:\Winbows\Perfectlylegitprogram.exe` 
	- Examine services' permissions: `sc.exe sdshow wuauserv`

- Output of the sdshow command: `D:(A;;CCLCSWRPLORC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOSDRCWDWO;;;WD)`

- Each object is a [securable object](https://learn.microsoft.com/en-us/windows/win32/secauthz/securable-objects), so it will have [security descriptor](https://learn.microsoft.com/en-us/windows/win32/secauthz/security-descriptors)

- Security descriptor contains two main parts: 
	- Discretionary Access Control List (DACL): specifies the access rights allowed or denied to particular users or groups
	- System Access Control List (SACL): specifies the types of access attempts that generate audit records for the object

- Security descriptor is written in ==Security Descriptor Definition Language (SDDL)== (search Internet for more)


## Examine service permissions using PowerShell

- `Get-Acl`: examine service permissions using that service's paths (`Get-ACL -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List`)

 - SID is written in SDDL

## References:

[Windows Fundamentals](https://academy.hackthebox.com/module/49/section/1016)