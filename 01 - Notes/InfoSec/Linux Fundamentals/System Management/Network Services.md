
2025-02-26 08:55

Tags: #linux #network  

## SSH

- SSH (Secure Shell): a network protocol that allows ==secure transmission== of data and commands over the network

- To use SSH, a SSH server must be active

- OpenSSH is the most used SSH server, free & open-source & encrypted connection, connect without being intercepted by third parties

- Connect to target: `ssh cry0l1t3@10.129.17.122`

- Can be configured in /etc/ssh/sshd_config

## NFS

- NFS (Network File System): allow user to ==manage files on remote systems== as if they are in the local system

- Efficiently manage files over the network

- Can be configured in /etc/exports


## Web Servers

- **Web servers**: *software* that ==delivers== data, documents, applications,... over the Internet (like a waiter)

- Use ==HTML== to transmit data (both send & receive) to/from clients (web browsers)

- Apache is a popular web server in Linux

- Python web server is also an option

- Utilities:
	- Facilitate file transfers
	- Enable tester to login and interact through HTTP or HTTPS ports
	- Leveraged to conduct phishing attacks
	- ...

- Can be configured in /etc/apache2/apache2.conf


## VPN

- VPN (Virtual Private Network): serves like an encrypted, hidden tunnel between client and server

- OpenVPN is an open-source option

- Can be configured in /etc/openvpn/server.conf

- Can use the .ovpn file



## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2094)
