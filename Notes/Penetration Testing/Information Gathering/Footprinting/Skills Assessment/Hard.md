
2025-09-16 10:27

Tags: #footprint #hands-on 

## Hard

- **Nmap**:
	- Port 22: Ssh
	- Port 143, 993: IMAP
	- Port 110, 995: POP3
	- UDP port 161: SNMP

- Remember to scan **UDP ports** too

- ![[Pasted image 20250916105752.png]]
- Found the community string **backup**

- Found the user `"tom NMds732Js2761"`

- Found only this message in his IMAP mailbox (means nothing):
	- ![[Pasted image 20250916162533.png]]

- Found the ssh private keys in **POP3**

- Ssh using that key to **root** user

- Get that info in `users.sql` file

## References:

https://academy.hackthebox.com/module/112/section/1080