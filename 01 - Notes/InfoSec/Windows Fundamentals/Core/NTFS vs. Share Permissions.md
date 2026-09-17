
2025-03-17 09:06

Tags: #windows  

## NTFS & SMB

- `Server Message Block protocol` (`SMB`): protocol used in Windows to connect ==shared resources== like files and printers

![[Pasted image 20250317090807.png]]

- Elaborate:
	- The client sends SMB request to work with file systems or printers remotely (open files, show contents,...)
	- The request is sent to the SMB file server (the server can be our target), then the server check the permission of the client, then it gets the data the client needs, or use the printers if the client is granted
	- The server then sends SMB response back to the client (the data which the client needs)

- ==When connect through SMB==, two types of permissions are applied: 
	- Share permission (applied when accessing resources over the network - SMB)
	- [NTFS permissions](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FWindows%20Fundamentals%2FFile%20System)(view in the link)

- ==Share permission== 

|Permission|Description|
|---|---|
|`Full Control`|Users are permitted to perform all actions given by Change and Read permissions as well as change permissions for NTFS files and subfolders|
|`Change`|Users are permitted to read, edit, delete and add files and subfolders|
|`Read`|Users are allowed to view file & subfolder contents|
- Some special permissions of NTFS (more control of the permissions) can be reviewed in the link below

## Creating a Network Share

- Create a shared folder:
	- Creating the Folder
	- ![[Pasted image 20250317100544.png]]
	- Making It a Share:
	- ![[Pasted image 20250317100600.png]]
	- Share Permissions ACL (Sharing Tab): An ACL (access control list) is set up for the share, similar to NTFS permissions
	- ![[Pasted image 20250317100652.png]]

- Using smbclient to list available shares: `smbclient -L SERVER_IP -U htb-student`

- Connecting to the Company Data share: `smbclient '\\SERVER_IP\Company Data' -U htb-student`

## Windows Defender Firewall Considerations

- Windows Defender Firewall may block SMB connections -> need to be configured

- Mounting the Share: create a mount point (a directory where shared external file is attached)
	- `sudo mount -t cifs -o username=htb-student,password=Academy_WinFun! //ipaddoftarget/"Company Data" /home/user/Desktop/`

- Monitoring Shared Resources (see more in the link):
	- net share: Lists all shared folders, including default shares like C$.
	- Computer Management: Provides detailed views of shared folders, sessions, and open files.
	- Event Viewer: view the logs in the system


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/1017)