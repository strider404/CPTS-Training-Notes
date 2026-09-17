
2025-03-10 09:46

Tags: #windows 

## Windows Versions

| Operating System Names               | Version Number |
| ------------------------------------ | -------------- |
| Windows NT 4                         | 4.0            |
| Windows 2000                         | 5.0            |
| Windows XP                           | 5.1            |
| Windows Server 2003, 2003 R2         | 5.2            |
| Windows Vista, Server 2008           | 6.0            |
| Windows 7, Server 2008 R2            | 6.1            |
| Windows 8, Server 2012               | 6.2            |
| Windows 8.1, Server 2012 R2          | 6.3            |
| Windows 10, Server 2016, Server 2019 | 10.0           |



## Accessing Windows

- Local access: directly interact with the system (ex: keyboard, mouse, Arduino)

- Remote access: interact over the network

- Remote access technologies:
	- Virtual Private Networks (VPN)
	- Secure Shell (SSH)
	- File Transfer Protocol (FTP)
	- Virtual Network Computing (VNC)
	- Windows Remote Management (or PowerShell Remoting) (WinRM)
	- Remote Desktop Protocol (RDP)


## Remote Desktop Protocol (RDP)

- RDP: client/server protocol that allow remote access to Windows system, listening on port 3389

- Built-in RDP in Windows: Remote Desktop Connection (mstsc.exe)

- Remote access must be allowed in the target system

- Information such as target hostnames, IP addresses, and sometimes even user credentials or specific configuration settings might be listed in the .rdp file


## xfreerdp

- xfreerdp: a tool to remote access to a Windows target from a Linux host

- Connect to a Windows target:
	- `xfreerdp /v:<targetIp> /u:htb-student /p:Password`


## Creating a Network Share

- 
## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/454)