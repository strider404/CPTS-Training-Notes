
2026-08-05 20:06

Tags: 

## Paper

- Nmap
	- ![[Pasted image 20260806105117.png]]
	- Port 22,80,443


- We got this page in port 80
	- ![[Pasted image 20260806110047.png]]
	- Catch the request with burp
	- ![[Pasted image 20260806110135.png]]
	- Notice the X-backend-server header is office.paper

- office.paper
	- ![[Pasted image 20260806110318.png]]
	- It is using Wordpress 5.2.3
	- ![](Pasted%20image%2020260806110548.png)
	- It is vulnerable to CVE-2019-17671 (using wpscan)
	- ![](Pasted%20image%2020260806113020.png)


- Exploit
	- Exploit that CVE by adding /?static=1&order=desc
	- ![](Pasted%20image%2020260806114017.png)
	- It displays the private post
	- Secret registration URL: http://chat.office.paper/register/8qozr226AhkCHZdyY
	- It's a rocket.chat server, register a clone account
	- Discover a group chat and the `recyclops` bot
	- ![](Pasted%20image%2020260806114755.png)
	- Chat with it 
	- ![](Pasted%20image%2020260806115017.png)
	- Discover a hubot configuration file
	- ![](Pasted%20image%2020260806115533.png)
	- recyclops:Queenofblad3s!23
	- ![](Pasted%20image%2020260806115744.png)
	- User: dwight
	- Tried to login to chat.office.paper, got ts
	- ![](Pasted%20image%2020260806115935.png)
	- lol


- SSH to that guy, worked 
	- ![](Pasted%20image%2020260806120136.png)
	- Polkit version: 0.115-6
	- ![](Pasted%20image%2020260806120619.png)
	- Vulnerable to CVE-2021-3560
	- Download a POC and exploit
	- ![](Pasted%20image%2020260806123244.png)

## References:

