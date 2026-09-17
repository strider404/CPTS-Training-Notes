
2026-06-29 16:48

Tags: #labs

## Cap

- Nmap scan: 
	- ![[Pasted image 20260629164841.png]]
	- 21,22,80

- Web:
	- ![[Pasted image 20260629164907.png]]
	- Run snapshot:
		- ![[Pasted image 20260629164936.png]]
	- Change the data to 0:
		- ![[Pasted image 20260629165000.png]]
	- Get valid pcap file, download it


- Get nathan's password in that file:
	- ![[Pasted image 20260629165032.png]]
	- Buck3tH4TF0RM3!

- SSH to the machine using that credential, run linpeass:
	- ![[Pasted image 20260629165134.png]]
	- Python with CAP_SETUID set
	- ![[Pasted image 20260629165315.png]]
	- Get the payload in GTFObin
	- ![[Pasted image 20260629165307.png]]


## References:

