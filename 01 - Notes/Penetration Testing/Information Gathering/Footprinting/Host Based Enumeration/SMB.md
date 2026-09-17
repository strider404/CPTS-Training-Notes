
2025-09-05 10:53

Tags: #footprint  

## SMB (Server Message Block)

- **Definition**: A client-server network protocol used for *sharing resources* like files, printers, and other network resources.

- **Port 139, 445**

- **Primary Use**: Predominantly used in Windows operating systems, but it is also available on other platforms.


- **Functionality**: It allows a client application to read, write, and access resources on a server. The connection is typically established over TCP, using a three-way handshake.


- **Access Control**: Access rights to shares are managed through Access Control Lists (ACLs), which can define permissions like read, execute, or full access for specific users and groups.


- **Versions**: SMB has evolved through several versions, each adding features and improvements:
	- **CIFS (SMB 1.0)**: An early version, now considered outdated.
	  
	- **SMB 2.x**: Introduced significant performance and security enhancements.
	  
	- **SMB 3.x**: Added features like end-to-end encryption, multichannel connections, and improved integrity checking.



## Samba

- **Definition**: A free software *re-implementation* of the SMB networking protocol that allows *Unix-like* systems (such as Linux) to interoperate with Windows-based systems.


- **CIFS**: Samba implements the *Common Internet File System (CIFS)* protocol, which is a specific dialect of SMB 1.0.


- **Functionality**:
	- Acts as a server to provide file and print services to SMB/CIFS clients.
	  
	- Can join a Windows workgroup or an Active Directory domain.
	  
	- Starting with version 4, Samba can function as an Active Directory domain controller.


- **Configuration**: Managed through the `/etc/samba/smb.conf` file, which contains global settings and definitions for individual shares.

- **Settings**:
![[Pasted image 20250905110139.png]]


- **Dangerous Settings**: Certain configurations in `smb.conf` can create security vulnerabilities. These include:
	- `guest ok = yes`: Allows anonymous access without a password.
	  
	- `writable = yes` / `read only = no`: Allows users to modify or create files.
	  
	- `browseable = yes`: Allows users to see the share in a list of available shares.


## Footprinting the Service

#### Nmap

- Into **p139, p445**
![[Pasted image 20250905110716.png]]


#### RPCclient

- **`rpcclient`**: Used to *perform MS-RPC functions* to **enumerate** domains, users, shares, and other server information
![[Pasted image 20250905113907.png]]

![[Pasted image 20250905112702.png]]


#### SMBClient

- Used to allow your machine to use **SMB/CIFS** (which is exclusively on Windows)

- **Listing shares:**
![[Pasted image 20250905115028.png]]
- `-N` is no password
- `-L` is listing shares (without it you must specific the share with `/` like in the below pic)

- **Connect to a share:**
![[Pasted image 20250905115858.png]]


- **Download file from SMB**:
![[Pasted image 20250905115053.png]]


#### Others

- **Impacket (`samrdump.py`)**: A collection of Python classes for working with network protocols, including tools for user enumeration.
![[Pasted image 20250905112912.png]]

- **`smbmap` & `CrackMapExec`**: Tools used to enumerate share permissions and other information.
![[Pasted image 20250905112943.png]]


- **`enum4linux-ng`**: An automated tool that combines many enumeration techniques to gather extensive information about users, shares, policies, and OS details.
![[Pasted image 20250905113010.png]]


## References:

