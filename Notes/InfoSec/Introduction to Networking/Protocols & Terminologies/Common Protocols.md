
2025-05-17 11:14

Tags: #network  

## Common Protocols

- **Internet protocols**: standardized rules and guidelines defined in RFCs that specify how devices on a network should communicate with each other

- Connection: *Wired / Wireless*

- **Main types**:
	- Transmission Control Protocol (TCP)
	- User Datagram Protocol (UDP)


## Transmission Control Protocol (TCP)

- **Reliable, connection-oriented**

- Uses a **Three-Way Handshake** to establish and maintain sessions.

|**Protocol**|**Acronym**|**Port**|**Description**|
|---|---|---|---|
|Telnet|`Telnet`|`23`|Remote login service|
|Secure Shell|`SSH`|`22`|Secure remote login service|
|Simple Network Management Protocol|`SNMP`|`161-162`|Manage network devices|
|Hyper Text Transfer Protocol|`HTTP`|`80`|Used to transfer webpages|
|Hyper Text Transfer Protocol Secure|`HTTPS`|`443`|Used to transfer secure webpages|
|Domain Name System|`DNS`|`53`|Lookup domain names|
|File Transfer Protocol|`FTP`|`20-21`|Used to transfer files|
|Trivial File Transfer Protocol|`TFTP`|`69`|Used to transfer files|
|Network Time Protocol|`NTP`|`123`|Synchronize computer clocks|
|Simple Mail Transfer Protocol|`SMTP`|`25`|Used for email transfer|
|Post Office Protocol|`POP3`|`110`|Used to retrieve emails|
|Internet Message Access Protocol|`IMAP`|`143`|Used to access emails|
|Server Message Block|`SMB`|`445`|Used to transfer files|
|Network File System|`NFS`|`111`, `2049`|Used to mount remote systems|
|Bootstrap Protocol|`BOOTP`|`67`, `68`|Used to bootstrap computers|
|Kerberos|`Kerberos`|`88`|Used for authentication and authorization|
|Lightweight Directory Access Protocol|`LDAP`|`389`|Used for directory services|
|Remote Authentication Dial-In User Service|`RADIUS`|`1812`, `1813`|Used for authentication and authorization|
|Dynamic Host Configuration Protocol|`DHCP`|`67`, `68`|Used to configure IP addresses|
|Remote Desktop Protocol|`RDP`|`3389`|Used for remote desktop access|
|Network News Transfer Protocol|`NNTP`|`119`|Used to access newsgroups|
|Remote Procedure Call|`RPC`|`135`, `137-139`|Used to call remote procedures|
|Identification Protocol|`Ident`|`113`|Used to identify user processes|
|Internet Control Message Protocol|`ICMP`|`0-255`|Used to troubleshoot network issues|
|Internet Group Management Protocol|`IGMP`|`0-255`|Used for multicasting|
|Oracle DB (Default/Alternative) Listener|`oracle-tns`|`1521`/`1526`|The Oracle database default/alternative listener is a service that runs on the database host and receives requests from Oracle clients.|
|Ingres Lock|`ingreslock`|`1524`|Ingres database is commonly used for large commercial applications and as a backdoor that can execute commands remotely via RPC.|
|Squid Web Proxy|`http-proxy`|`3128`|Squid web proxy is a caching and forwarding HTTP web proxy used to speed up a web server by caching repeated requests.|
|Secure Copy Protocol|`SCP`|`22`|Securely copy files between systems|
|Session Initiation Protocol|`SIP`|`5060`|Used for VoIP sessions|
|Simple Object Access Protocol|`SOAP`|`80`, `443`|Used for web services|
|Secure Socket Layer|`SSL`|`443`|Securely transfer files|
|TCP Wrappers|`TCPW`|`113`|Used for access control|
|Internet Security Association and Key Management Protocol|`ISAKMP`|`500`|Used for VPN connections|
|Microsoft SQL Server|`ms-sql-s`|`1433`|Used for client connections to the Microsoft SQL Server.|
|Kerberized Internet Negotiation of Keys|`KINK`|`892`|Used for authentication and authorization|
|Open Shortest Path First|`OSPF`|`89`|Used for routing|
|Point-to-Point Tunneling Protocol|`PPTP`|`1723`|Is used to create VPNs|
|Remote Execution|`REXEC`|`512`|This protocol is used to execute commands on remote computers and send the output of commands back to the local computer.|
|Remote Login|`RLOGIN`|`513`|This protocol starts an interactive shell session on a remote computer.|
|X Window System|`X11`|`6000`|It is a computer software system and network protocol that provides a graphical user interface (GUI) for networked computers.|
|Relational Database Management System|`DB2`|`50000`|RDBMS is designed to store, retrieve and manage data in a structured format for enterprise applications such as financial systems, customer relationship management (CRM) systems.|

## User Datagram Protocol (UDP)

- **Unreliable, connectionless** (connectionless: sends the data packets to the destination without checking to see if they were received)

- Some packets can be lost on the way (*Packet loss*)

- Faster, used when **speed > reliability** (e.g., video streaming).

|**Protocol**|**Acronym**|**Port**|**Description**|
|---|---|---|---|
|Domain Name System|`DNS`|`53`|It is a protocol to resolve domain names to IP addresses.|
|Trivial File Transfer Protocol|`TFTP`|`69`|It is used to transfer files between systems.|
|Network Time Protocol|`NTP`|`123`|It synchronizes computer clocks in a network.|
|Simple Network Management Protocol|`SNMP`|`161`|It monitors and manages network devices remotely.|
|Routing Information Protocol|`RIP`|`520`|It is used to exchange routing information between routers.|
|Internet Key Exchange|`IKE`|`500`|Internet Key Exchange|
|Bootstrap Protocol|`BOOTP`|`68`|It is used to bootstrap hosts in a network.|
|Dynamic Host Configuration Protocol|`DHCP`|`67`|It is used to assign IP addresses to devices in a network dynamically.|
|Telnet|`TELNET`|`23`|It is a text-based remote access communication protocol.|
|MySQL|`MySQL`|`3306`|It is an open-source database management system.|
|Terminal Server|`TS`|`3389`|It is a remote access protocol used for Microsoft Windows Terminal Services by default.|
|NetBIOS Name|`netbios-ns`|`137`|It is used in Windows operating systems to resolve NetBIOS names to IP addresses on a LAN.|
|Microsoft SQL Server|`ms-sql-m`|`1434`|Used for the Microsoft SQL Server Browser service.|
|Universal Plug and Play|`UPnP`|`1900`|It is a protocol for devices to discover each other on the network and communicate.|
|PostgreSQL|`PGSQL`|`5432`|It is an object-relational database management system.|
|Virtual Network Computing|`VNC`|`5900`|It is a graphical desktop sharing system.|
|X Window System|`X11`|`6000-6063`|It is a computer software system and network protocol that provides GUI on Unix-like systems.|
|Syslog|`SYSLOG`|`514`|It is a standard protocol to collect and store log messages on a computer system.|
|Internet Relay Chat|`IRC`|`194`|It is a real-time Internet text messaging (chat) or synchronous communication protocol.|
|OpenPGP|`OpenPGP`|`11371`|It is a protocol for encrypting and signing data and communications.|
|Internet Protocol Security|`IPsec`|`500`|IPsec is also a protocol that provides secure, encrypted communication. It is commonly used in VPNs to create a secure tunnel between two devices.|
|Internet Key Exchange|`IKE`|`11371`|It is a protocol for encrypting and signing data and communications.|
|X Display Manager Control Protocol|`XDMCP`|`177`|XDMCP is a network protocol that allows a user to remotely log in to a computer running the X11.|

## ICMP

- **Internet Control Message Protocol (ICMP)**: protocol used by devices to *communicate* with each other on the Internet for various purposes (network diagnostics, error reporting)

- *Versions*:
	- **ICMPv4** – for IPv4
	- **ICMPv6** – for IPv6

- Sends *requests* and *messages* between devices

- **ICMP Requests**: a message sent by one device to another to request information or perform a specific action (e.g., ping)

- **ICMP Messages**: either a request or a reply
	- Error messages, `destination unreachable`, and `time exceeded` messages

|**Request Type**|**Description**|
|---|---|
|`Echo Request`|This message tests whether a device is reachable on the network. When a device sends an echo request, it expects to receive an echo reply message. For example, the tools `tracert` (Windows) or `traceroute` (Linux) always send ICMP echo requests.|
|`Timestamp Request`|This message determines the time on a remote device.|
|`Address Mask Request`|This message is used to request the subnet mask of a device.|

|**Message Type**|**Description**|
|---|---|
|`Echo reply`|This message is sent in response to an echo request message.|
|`Destination unreachable`|This message is sent when a device cannot deliver a packet to its destination.|
|`Redirect`|A router sends this message to inform a device that it should send its packets to a different router.|
|`time exceeded`|This message is sent when a packet has taken too long to reach its destination.|
|`Parameter problem`|This message is sent when there is a problem with a packet's header.|
|`Source quench`|This message is sent when a device receives packets too quickly and cannot keep up. It is used to slow down the flow of packets.|

- **Time-To-Live (TTL)**: (in the ICMP packet header) limits the packet's lifetime as it travels through the network
	- Each time a packet passes through a router, TTL = TTL - 1
	- TTL == 0 =>discards the packet and sends an ICMP `Time Exceeded` message back to the sender

- *Can use TTL to check the OS type*, cause every OS has a default value of TTL
	- e.g., if TTL = 122 => could be Windows because Windows default TTL = 128
	- **Windows TTL=128, Linux TTL=64**


## VoIP

- **Voice over Internet Protocol (VoIP)**: a method of transmitting voice and multimedia communications

- Allows voice/multimedia (video, messages) communication over IP networks (e.g., Skype, Zoom).

- Uses **SIP** (Session Initiation Protocol) primarily on ports **5060/5061**.

- Uses **requests** and **methods** between the endpoints

|**Method**|**Description**|
|---|---|
|`INVITE`|Initiates a session or invites another endpoint to participate.|
|`ACK`|Confirms the receipt of an INVITE request.|
|`BYE`|Terminate a session.|
|`CANCEL`|Cancels a pending INVITE request.|
|`REGISTER`|Registers a SIP user agent (UA) with a SIP server.|
|`OPTIONS`|Requests information about the capabilities of a SIP server or user agent, such as the types of media it supports.|

- **SIP enumeration** (e.g., using `OPTIONS` to probe users or systems).

- Config files like `SEPxxxx.cnf` may reveal IP phone configurations.

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1872)