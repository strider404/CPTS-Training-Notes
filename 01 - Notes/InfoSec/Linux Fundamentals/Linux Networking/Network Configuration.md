
2025-03-03 09:48

Tags: #linux #network  #hands-on 

## Network

- Configure Lixux for NAC needs: 
	- SELinux (Security-Enhanced Linux): set up security policies
	- AppArmor: application security
	- TCP wrappers: control access to a service by IP address
	- syslog, rsyslog, ss (for socket statistics), lsof (to list open files), and the ELK stack (Elasticsearch, Logstash, and Kibana): monitor & analyze network traffic

- **Netmask**: 32-bits to distinguish the network and the host in an IP address
	- 1 means the network
	- 0 means the host
	- Ex: 192.168.1.5 with subnet mask 255.255.255.0 (11111111.11111111.11111111.00000000) means: the network is 192.168.1.0, the host is 5

- **DNS** (Domain Name System): translate web's domain name into IP address


## Configuring Network Interfaces

- Obtain info: `ip addr`

- Activate Network Interface: `sudo ip link set eth0 up`

- Assign IP Address & netmask to an Interface: `sudo ip addr add 192.168.1.2/24 dev eth0`
	- 192.168.1.2: IP address
	- /24: netmask

- Assign the Route to an Interface: `sudo route add default gw 192.168.1.1 eth0`
	- set the default gateway for a network interface

- Editing DNS setting: `sudo vim /etc/resolv.conf`
	- change the nameserver to the desired DNS server
	- Won't be saved after reboots

- Editing Interfaces: `sudo vim /etc/network/interfaces`
	- Can change the IP address, netmask, gateway, DNS server of a network protocol
	- Need to restart after
	- Saved even after reboots

- Restart Networking Service: `sudo systemctl restart networking`


## Network Access Control

- Network access control (NAC): restricting who can / cannot access & configure the network

- Types of NAC:

| Type                                 | Description                              |
| ------------------------------------ | ---------------------------------------- |
| Discretionary Access Control (`DAC`) | The owner sets the permissions           |
| Mandatory Access Control (`MAC`)     | The OS sets the permission               |
| Role-Based Access Control (`RBAC`)   | Permissions assign by roles of the users |

 - DAC: 
	 - Users or groups who own the resources can set permissions to allow/forbid other users/groups

- MAC: 
	- Each resource has a security label, and each user has a security clearance represent its security level
	- If the security level of the security clearance is >= the security label of the resource, that user gains the permission

- RBAC:
	- Users are assigned to specific roles, and can only access the resources they need


## Monitoring

- Network monitoring: capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior


## Troubleshooting

- Network troubleshooting: diagnosing & resolving network problems

- Tools: 
	-  Ping
	- Traceroute
	- Netstat
	- Tcpdump
	- Wireshark
	- Nmap

## Hardening

- Security-Enhanced Linux: mandatory access control (`MAC`) system integrated into the Linux kernel, secured at low level, hard to configure

- AppArmor: also mandatory access control (`MAC`) system, but work as a kernel module and easier to operate, but not as secured

- TCP Wrappers: host-based network control tool that restricts network connections via IP addresses of incoming connections

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2098)
