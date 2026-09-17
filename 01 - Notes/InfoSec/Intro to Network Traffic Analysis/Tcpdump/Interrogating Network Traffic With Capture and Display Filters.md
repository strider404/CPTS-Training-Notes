
2025-06-27 09:56

Tags: #network #hands-on 

## Task 2

- What type of traffic do we see?

- Common Protocols
	- HTTPS, DNS, HTTP, IP, TCP, UDP, DNS

- Ports utilized
	- 443, 53, 80, random ports

## Task 3

- Are you noticing any common connections between a server and host? If so, who?

- What are the client and server port numbers used in the first full TCP three-way handshake?
	- Client: 43804
	- Server: 80

- Who are the servers in these conversations? How do we know?
	- Servers will use ports like HTTP and HTTPS
		- 13.35.106.128
		- 72.21.91.29
		- 95.216.26.30
		- 207.244.88.140
		- 64.233.177.100
		- 108.177.122.95
		- 151.139.128.14
		- 142.250.9.94
		- 74.125.138.95
		- ....

- Who are the receiving hosts?
	- 172.16.146.2

## Task 4

- What is the timestamp of the first established conversation in the pcap file?
	- 2021-05-11 22:34:01.401270

- What is the IP address/s of apache.org from the DNS server responses?
	- 95.216.26.30
	- 207.244.88.140

- What protocol is being utilized in that first conversation? (name/#)
	- HTTP/80

## Task 5

- Who is the DNS server for this segment?
	- 172.16.146.1

- What domain name/s were requested in the pcap file?
	- apache.org.
	- fonts.googleapis.com.
	- cse.google.com.
	- ocsp.sectigo.com.
	- www.youtube.com.
	- ....

- What type of DNS Records could be seen?
	- A
	- AAAA
	- CNAME

-  Who requests an A record for apache.org? (hostname or IP)
	- 172.16.146.2

- What information does an A record provide?
	- IPv4 Address

- Who is the responding DNS server in the pcap? (hostname or IP)
	- 172.16.146.1

## Task 6

- What are the most common HTTP request methods from this PCAP?
	- POST

- What is the most common HTTP response from this PCAP?
	- 200 OK
## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/81/section/787)