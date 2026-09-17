
2025-04-03 11:05

Tags: #windows #shell  #hands-on

## Types of Information

![[Pasted image 20250403110708.png]]



## Getting System Information

- **`systeminfo`** – Retrieves comprehensive host details (OS version, hostname, hotfixes, etc.)

- **`hostname`** – Displays the machine’s hostname.

- **`ver`** – Shows the OS version.


## Getting Network Information

- **`ipconfig`**: Displays network configurations (IP addresses, subnet, gateway, DNS).
	- **`ipconfig /all`**: Provides detailed network adapter information, including MAC addresses and DHCP settings.

- **`arp /a`**: Lists devices that have communicated with the system


## Getting User Information

- `whoami`: reveals the current domain and username
	- `whoami /priv` displays security privileges
	- `whoami /groups` lists the groups the user belongs to
	- `whoami /all`: gather all of those information at once

- `net user` shows all user accounts on the system

- `net group` (for domains) and `net localgroup` (for local machines) display available groups

- `net share` lists shared resources accessible to the user.

- `net view` provides an overview of network-wide shared resources.


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1608)