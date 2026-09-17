
2025-03-24 10:22

Tags: #windows  

## Desktop Experience vs. Server Core

- Windows Server Core: ==minimal installation== with only essential server functions
	- Less resources needed
	- Smaller attack surface
	- Use command-line tools (Sconfig)

- Server core vs Desktop applications:

| **Application**                    | **Server Core** | **Desktop Experience** |
| ---------------------------------- | --------------- | ---------------------- |
| Command prompt                     | Available       | Available              |
| Windows PowerShell/ Microsoft .NET | Available       | Available              |
| Regedit                            | Available       | Available              |
| Diskmgmt.msc                       | Not Available   | Available              |
| Server Manager                     | Not Available   | Available              |
| Mmc.exe                            | Not Available   | Available              |
| Eventvwr                           | Not Available   | Available              |
| Services.msc                       | Not Available   | Available              |
| Control Panel                      | Not Available   | Available              |
| Windows Explorer                   | Not Available   | Available              |
| Taskmgr                            | Available       | Available              |
| Internet Explorer or Edge          | Not Available   | Available              |
| Remote Desktop Services            | Available       | Available              |


## References:

[Windows Fundamentals](https://academy.hackthebox.com/module/49/section/465)