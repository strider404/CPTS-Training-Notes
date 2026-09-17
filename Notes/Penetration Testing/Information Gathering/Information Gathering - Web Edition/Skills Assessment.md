
2025-09-25 14:50

Tags: #web #hands-on 

## Skills Assessment

- **Append the IP address to the list of host (Important)**
	- `sudo sh -c "echo '83.136.250.223 inlanefreight.htb' >> /etc/hosts"`
	- If you don't do this, you will **never** find the unknown **vhost**

- **Whois** the inlanefreight.com get IANA ID

- `curl` to get the **nginx**

- Find **vhosts** using `subdomains-top1million-110000.txt` wordlist with **gobuster** to get the directories
	- ![[Pasted image 20250925183128.png]]


- Found **robots.txt** in that vhost
	- ![[Pasted image 20250927134204.png]]

- **ADD found vhost next to default vhost** 
	- ![[Pasted image 20250927142454.png]]
	  

- Found the **robots.txt**
	- ![[Pasted image 20250927143351.png]]
	- ![[Pasted image 20250927142413.png]]


- **Discover another vhost in web1337**
	- ![[Pasted image 20250929092729.png]]
	- **Add to /etc/hosts/**


- Crawled that vhost with **ReconSpider** and found the email address
	- ![[Pasted image 20250929093415.png]]


- And the new API too
## References:

