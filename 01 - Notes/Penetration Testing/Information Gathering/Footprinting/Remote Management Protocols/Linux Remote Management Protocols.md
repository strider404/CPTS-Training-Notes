
2025-09-12 10:45

Tags: #footprint  

## SSH (Secure Shell)

- **Function:** Enables a secure, encrypted connection between two computers over an insecure network for command-line access, file transfers, and port forwarding.

- **Default Port**: TCP 22.

- **Versions:**
	- **SSH-1:** vulnerable to *Man-in-the-Middle (MITM) attacks.*
	- **SSH-2:** more advanced and secure

- **Authentication Methods:**
	- Password authentication
	  
	- Public-key authentication
	  
	- Host-based authentication
	  
	- Keyboard authentication
	  
	- Challenge-response authentication
	  
	- GSSAPI authentication


- **Public-Key Authentication:** This method is highlighted as a secure alternative to passwords. It involves a *unique public-private key pair.* The private key is stored on the **client** and is protected by a passphrase, while the public key is stored on the server. The client proves its identity by **solving a cryptographic challenge from the server with the private key**

#### Configuration

- Stored in `/etc/ssh/sshd_config`

- **Dangerous settings:**
	- `PermitRootLogin yes`: Allows direct login as the root user, which is highly risky.
    
	- `PasswordAuthentication yes`: Enables password logins, which can be vulnerable to brute-force attacks.
    
	- `PermitEmptyPasswords yes`: Allows logins with no password.
    
	- `Protocol 1`: Allows the use of the outdated and insecure SSHv1.

#### Footprinting

- The SSH **banner** often reveals the **version** (e.g., `OpenSSH_8.2p1`), which can be checked for known vulnerabilities.

- Tools like **ssh-audit** can check server configurations for weak encryption algorithms and other security issues.
	- ![[Pasted image 20250912150102.png]]

- We can **specify the authentication method**
	- ![[Pasted image 20250912150201.png]]
## Rsync

- **Function**: A tool for efficiently **copying and synchronizing files locally or between remote hosts**. It is known for its **delta-transfer algorithm**, which only sends the differences between files to save bandwidth.

- **Default Port**: TCP **873**.

- **Security**:
	- By default, it can operate without authentication.
	  
	- It can be configured to run securely over an established SSH connection.

- **Vulnerabilities**:
	- If misconfigured, an attacker can **list and download files from an rsync share** without authentication.
	  
	- Reusing credentials found elsewhere might grant access to sensitive files on a secured rsync server.

#### Footprinting

- **Enumeration**:
	- Use **Nmap** to scan for an open port 873.
	  
	- Use tools like **Netcat (`nc`)** or the `rsync` command itself to probe for accessible shares and list their contents.
		- ![[Pasted image 20250912150718.png]]


## R-Services

- **Function**: An outdated suite of services (`rlogin`, `rsh`, `rexec`) for remote access between Unix systems. They have been largely replaced by SSH.

- **Ports**:
	- **512/TCP (`rexec`)**: Remote execution.
	- **513/TCP (`rlogin`)**: Remote login.
	- **514/TCP (`rsh`)**: Remote shell.

- **Security**:
	- **Highly insecure**: Transmits all data, including credentials, in **unencrypted cleartext**.
	- Vulnerable to MITM attacks.

- **Vulnerabilities**:
	- Authentication is based on a **"trusted host"** model using the `/etc/hosts.equiv` and `~/.rhosts` files.
	- Misconfigurations in these files, especially using the `+` wildcard, can allow any user from any host to log in without a password.

#### Footprinting

- **Enumeration**:
	- Use **Nmap** to find open ports 512, 513, and 514.
	  
	- If a trusted relationship is misconfigured, use `rlogin -l <username> <target_ip>` to attempt a passwordless login.
		- ![[Pasted image 20250912151053.png]]
		  
	- Commands like `rwho` and `rusers` can be used to gather information about logged-in users on the network.
		- ![[Pasted image 20250912151106.png]]
## References:

https://academy.hackthebox.com/module/112/section/1240