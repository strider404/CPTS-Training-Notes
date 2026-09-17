 
2025-06-23 10:47

Tags: #network #hands-on 

## Skills Assessment

- First: `ifconfig` to display network interfaces

![[Pasted image 20250623105349.png]]

- `netstat -tulnp4` to see open/listening ports

![[Pasted image 20250623112352.png]]

![[Pasted image 20250623112402.png]]


- `ping`: *test* the reachability of a host on a network (sending packets to another host), to confirm that our host can reach the target

![[Pasted image 20250623114258.png]]


- `nmap`: to see open ports on target machine
![[Pasted image 20250623172414.png]]


#### FTP (File Transfer Protocol) and HTTP (Hyper-Text Transport Protocol.)

- `nmap -p21,80 -sC -sV <target ip>`: -sC, -sV to get more info and version of the port 21 (FTP) and 80 (HTTP)

![[Pasted image 20250624171358.png]]

- Port 21 (FTP) is opened for everyone under `anonymous` user name

- SO we'll connect to it using `netcat` (make raw TCP/UDP connections)
![[Pasted image 20250624171629.png]]

- Login with *Passive mode* (each command in FTP must have `[Ctrl+V][Enter][Enter]` in the end):
![[Pasted image 20250624171653.png]]

- **FTP** (File Transfer Protocol) uses *two separate channels* to function.

| **Channel**     | **Purpose**                                       | **Port**                                              |
| --------------- | ------------------------------------------------- | ----------------------------------------------------- |
| Control Channel | Sends FTP commands (USER, PASS, LIST, RETR, etc.) | Port 21                                               |
| Data Channel    | Transfers files and directory listings            | Dynamic Port (Varies by mode: *Active* or *Passive*). |
![[Pasted image 20250624171925.png]]
- *Calculate Data Channel Port*: The 2 last number of PASV (194 and 40) => `194*256 +40`

- Needs to connect to the Data channel in new terminal:
![[Pasted image 20250624172109.png]]

- Use `LIST` in the Control channel to list available FTP files
![[Pasted image 20250624172207.png]]

- The file is shown in the Data Channel 
![[Pasted image 20250624172403.png]]
- Then start the Control channel again using previous commands, then use RETR to retrieve the file
![[Pasted image 20250624172330.png]]

- Connect to HTTP:
![[Pasted image 20250624172627.png]]

- `GET /` is an HTTP request that tells a web server "Give me the homepage (root directory) of this website."

- `Host` header tells the server which host we are requesting (it is possible for a server to host multiple, unique webpages all on the same server).

- `User Agent` header is used to indicate the agent making the web request

- `Content-Type` header tells us what type of data the server is replying with

- `Accept` header tells us what type of data it is able to receive,
#### Analysis

- **lo:**
	- Is the *loopback address*, the IP address the host used to *send data to itself*
	- Used when the applications in the same machine need to interact with each other, or for testing if the app works as intended, or for security (it loops, so the outside can't listen to it)
	- IP: `127.0.0.1`, Hostname: `localhost` (as resolved in the Local Address column of netstat)

- **ens3:**
	- *Public IP address*
	- To access the Internet
	- Hostname: The computer's hostname

- **tun0:**
	- *VPN tunnel*

- Port 135, 139, 445 will be opened in Windows host

- Port 3389: RDP

- Port 5357: Microsoft's Web Services for Devices API


## References:

