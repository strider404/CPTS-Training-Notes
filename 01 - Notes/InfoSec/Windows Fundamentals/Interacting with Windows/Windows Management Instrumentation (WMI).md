
2025-03-22 17:39

Tags: #windows  

## Windows Management Instrumentation (WMI)

- Windows Management Instrumentation (WMI) is a PowerShell subsystem providing robust system monitoring & management tools
	- WMI is a ==built-in Windows feature that PowerShell can interact with==
	- Provides query, manage, and automate system settings

 - Is a core part of Windows

- Components:

| **Component Name** | **Description**                                                                                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WMI service        | The ==Windows Management Instrumentation process==, which runs automatically at boot and acts as an intermediary between WMI providers, the WMI repository, and managing applications. |
| Managed objects    | ==Any logical or physical components== that can be managed by WMI.                                                                                                                     |
| WMI providers      | ==Objects that monitor== events/data related to a specific object.                                                                                                                     |
| Classes            | These are used by the WMI providers to ==pass data to the WMI service==.                                                                                                               |
| Methods            | These are attached to classes and allow ==actions== to be performed. For example, methods can be used to start/stop processes on remote machines.                                      |
| WMI repository     | A ==database== that stores all static data related to WMI.                                                                                                                             |
| CIM Object Manager | The system that ==requests data== from WMI providers and ==returns== it to the application requesting it.                                                                              |
| WMI API            | Enables applications to ==access the WMI infrastructure==.                                                                                                                             |
| WMI Consumer       | Sends ==queries== to objects via the CIM Object Manager.                                                                                                                               |

 - `wmic /?` to get aliases

- Use with Powershell: `Get-WmiObject`
	- -Class win32_OperatingSystem: get OS's info
	- -Class win32_Process: list processes
	- -Class win32_Service: list services
	- -Class win32_Bios: get BIOS info
	- -Class win32_useraccount: get User info (name, sid,...)
	- -Class win32_group: get Group info

- Call methods of WMI objects: `Invoke-WmiMethod`

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/461)
