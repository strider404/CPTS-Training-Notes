
2025-04-21 11:08

Tags: #windows #shell  #hands-on 

## Typical Protocols

| **Protocol** | **Description**                                                                          |
| ------------ | ---------------------------------------------------------------------------------------- |
| `SMB`        | For resource and file sharing.                                                           |
| `Netbios`    | An alternative name identification service when DNS fails.                               |
| `LDAP`       | Used for authentication and authorization with directory services like Active Directory. |
| `LLMNR`      | A fallback name resolution service for local networks.                                   |
| `DNS`        | The standard for resolving hostnames to IP addresses.                                    |
| `HTTP/HTTPS` | For requesting resources over the internet.                                              |
| `Kerberos`   | A network authentication protocol, primarily used with Active Directory                  |
| `WinRM`      | A protocol for remote hardware and software management.                                  |
| `RDP`        | Provides a graphical user interface for remote host access.                              |
| `SSH`        | A secure protocol for remote access, file transfers, and communication.                  |

## Local vs. Remote Access

#### Local Access

- *Local Access*: directly use the PC

- **Query Networking Settings**
	- `ipconfig`: Displays *basic network interface settings* like IP addresses, subnet masks, and default gateways.
	- **`arp -a`**: Shows the ARP (Address Resolution Protocol) cache, which *maps IP addresses to physical (MAC) addresses* of recently communicated-with hosts.
	- **`nslookup`**: A tool to query DNS servers to resolve hostnames to IP addresses and vice-versa.
	- **`netstat -an`**: Lists all active network connections and listening ports on the host.

#### PowerShell Net Cmdlets

|**Cmdlet**|**Description**|
|---|---|
|`Get-NetIPInterface`|Retrieve all `visible` network adapter `properties`.|
|`Get-NetIPAddress`|Retrieves the `IP configurations` of each adapter. Similar to `IPConfig`.|
|`Get-NetNeighbor`|Retrieves the `neighbor entries` from the cache. Similar to `arp -a`.|
|`Get-Netroute`|Will print the current `route table`. Similar to `IPRoute`.|
|`Set-NetAdapter`|Set basic adapter properties at the `Layer-2` level such as VLAN id, description, and MAC-Address.|
|`Set-NetIPInterface`|Modifies the `settings` of an `interface` to include DHCP status, MTU, and other metrics.|
|`New-NetIPAddress`|Creates and configures an `IP address`.|
|`Set-NetIPAddress`|Modifies the `configuration` of a network adapter.|
|`Disable-NetAdapter`|Used to `disable` network adapter interfaces.|
|`Enable-NetAdapter`|Used to turn network adapters back on and `allow` network connections.|
|`Restart-NetAdapter`|Used to restart an adapter. It can be useful to help push `changes` made to adapter `settings`.|
|`test-NetConnection`|Allows for `diagnostic` checks to be ran on a connection. It supports ping, tcp, route tracing, and more.|

- Details in the link

#### Remote access

- *Remote access*: using PC resources remotely (online), using SSH, RDP

- **SSH**: details about how to set up in the link
	- The commands to connect is *identical as the one in Linux*


- **WinRM** (Windows Remote Management): A protocol for remote hardware and software management (port 5985 & 5986)
	- **Testing:** Use `Test-WSMan -ComputerName <IP>` to check if the WinRM service is running on the target.
	- **Creating a Session:** Use the `Enter-PSSession -ComputerName <IP> -Credential <user>` cmdlet to start an interactive PowerShell session on the remote host. This can be done from both Windows and Linux hosts that have PowerShell installed.
		- `-Authentication Negotiate`: choose the most secure authentication protocol (mostly Kerberos)


## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1626)
