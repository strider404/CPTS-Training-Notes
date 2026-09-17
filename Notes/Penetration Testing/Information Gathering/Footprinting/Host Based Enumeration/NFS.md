
2025-09-05 14:50

Tags: #footprint  

## NFS

- **Purpose**: **NFS** (Network File System) is a *distributed file system protocol* that allows a user on a client computer to access files over a network as if they were on their local storage.


- **Usage**: It is primarily used between **Linux** and Unix-based systems.


- **Protocol**: It operates *differently* from SMB, so an NFS client cannot directly communicate with an SMB server. It is based on the Open Network Computing Remote Procedure Call (ONC-RPC) protocol.


## Versions

- **NFSv2**: An older version that initially operated over UDP and is widely supported.
  
- **NFSv3**: Added features like variable file size and improved error reporting. It is not fully compatible with NFSv2.

- **NFSv4**: A major update that introduced significant improvements:
	- **Security**: Includes Kerberos authentication and is stateful.
	- **Firewall-Friendly**: Uses only a single **TCP/UDP port (2049),** simplifying firewall configurations.
	- **Features**: Supports Access Control Lists (ACLs), provides performance enhancements, and no longer requires a portmapper.
	- **Authentication**: Requires user authentication, similar to SMB, unlike older versions which authenticated the client computer.

- **NFSv4.1**: Aims to support clustered server deployments, including scalable parallel access to files (pNFS extension).

- **Ports**:
	- *NFSv2 and NFSv3*: port **111**
	- *NFSv4*: port **2049**

#### Authentication & Authorization

- **Mechanism**: NFS itself has *no built-in authentication*; it relies on the underlying RPC protocol.
  
- **Common Method**: The most common method uses UNIX **UID (User ID)** and **GID (Group ID)**. The server trusts the client to provide correct user information.
  
- **Security Flaw**: A significant security issue arises if the client and server do not have the same UID/GID mappings. An attacker can *create a local user with a specific UID* (e.g., UID 0 for root) on their machine to gain corresponding privileges on the NFS share. Because of this, this authentication method should only be used in trusted networks.


#### Configuration

- **Configuration File**: NFS shares are configured in the `/etc/exports` file.
![[Pasted image 20250905150457.png]]

- **Dangerous Options**:
	- `insecure`: Allows client connections from ports above 1024.
	- `no_root_squash`: This is highly dangerous. By default, a remote root user (UID 0) is "squashed" and mapped to an anonymous, unprivileged user. This option disables that protection, allowing a remote root user to have full root privileges on the mounted filesystem.

## Footprinting the Service

- **Footprinting**: The key ports to scan for are TCP/UDP **111** (rpcbind/portmapper) and **2049** (nfs).

- **Tools**:
	- **Nmap**: Can be used with scripts like `rpcinfo` and `nfs*` to discover RPC services, list available shares, and view their contents.
		- `rpcinfo` NSE script retrieves a list of all currently running RPC services
			- ![[Pasted image 20250905152839.png]]
			  
	- **showmount**: The command `showmount -e <IP_ADDRESS>` lists all available shares from a target server. (from nsf-common package)
		- ![[Pasted image 20250905151158.png]]

- **Mounting**:
	1. Create a local directory on the client machine (e.g., `mkdir /mnt/target-nfs`).
	   
	2. Use the `mount` command to attach the remote share to the local directory (e.g., `sudo mount -t nfs <IP>:/<share_path> /mnt/target-nfs`).
		1. ![[Pasted image 20250905151259.png]]


- **Access**: Once mounted, you can interact with the files as if they were on your local system, subject to the permissions configured on the server. You can use `ls -n` to view the **numeric UID/GID** of file owners to *create corresponding local users for privilege escalation.*
	- ![[Pasted image 20250905151534.png]]


- **Unmounting**: The `umount` command is used to detach the share.
## References:

https://academy.hackthebox.com/module/112/section/1068