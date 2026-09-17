- Nmap scan
	- ![](Pasted%20image%2020260811163230.png)
	- ![](Pasted%20image%2020260811163530.png)
	- A convert web => PDF page
	- Running with Phusion Passenger 6.0.15
	- ![](Pasted%20image%2020260811163554.png)
	- Running with ruby
	- ![](Pasted%20image%2020260811163749.png)


- Set up a http server with python
	- ![](Pasted%20image%2020260811164355.png)
	- Use that to fetch
	- ![](Pasted%20image%2020260811164410.png)
	- ![](Pasted%20image%2020260811164426.png)
	- File's metadata using exiftool
	- ![](Pasted%20image%2020260811164512.png)
	- Generated with pdfkit 0.8.6
	- Vulnerable to CVE-2022-25765


- Exploit
	- Download the POC
	- ![](Pasted%20image%2020260811164724.png)
	- Exploit
	- ![](Pasted%20image%2020260811165303.png)
	- ![](Pasted%20image%2020260811165312.png)
	- Got the rev shell and upgrade it with python3
	- Find the hidden .bundle (use by Bundler to manage gem)
	- ![](Pasted%20image%2020260811165720.png)
	- In that dir contain a config file with the password for henry user
	- henry:Q3c1AqGHtoI0aXAYFH
	- Get the user flag through ssh

- Escalation
	- sudo -l
	- ![](Pasted%20image%2020260811165943.png)
	- henry can run `/usr/bin/ruby /opt/update_dependencies.rb` without password
	- This script reads file dependencies.yml
	- ![](Pasted%20image%2020260811171559.png)
	- It is using ruby 2.7.4
	- ![](Pasted%20image%2020260811171739.png)
	- Which is vulnerable to this [payload](https://staaldraad.github.io/post/2021-01-09-universal-rce-ruby-yaml-load-updated/) using yaml files
	- ![](Pasted%20image%2020260811171802.png)
	- And we get the RCE
	- ![](Pasted%20image%2020260811172057.png)
	- Change the git_set with cat /root/root.txt and we get the root flag