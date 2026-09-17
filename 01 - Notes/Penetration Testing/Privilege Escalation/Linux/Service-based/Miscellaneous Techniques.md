
2026-05-15 16:55

Tags: #escalation  

## Passive Traffic Capture

- **Concept:** Unprivileged users may capture sensitive network traffic if tools like `tcpdump` are installed and accessible.


- **Useful Tools:** `net-creds`, `PCredz`.


- **Target Data:**
    - **Cleartext Credentials:** Captured from unencrypted protocols like HTTP, FTP, POP, IMAP, Telnet, or SMTP.
        
    - **Hashes:** Kerberos, SMBv2, or Net-NTLMv2 hashes that can be subjected to offline brute-force attacks.
        
    - **Other Sensitive Info:** Credit card numbers, SNMP community strings.


## Weak NFS Privileges

- **Concept:** Network File System (NFS) operates on TCP/UDP port 2049. Misconfigurations in the export list (`/etc/exports`) can allow remote users to execute code as root.


- **Key Vulnerability:** The `no_root_squash` option. By default, NFS uses `root_squash` to downgrade remote root users to an unprivileged account (`nfsnobody`). If `no_root_squash` is enabled, a remote root user can create files on the share that remain owned by root.


- **Exploitation Steps:**
    1. **Enumerate:** List available NFS shares using `showmount -e <target_IP>`.
        
    2. **Create Payload:** Write a C script that spawns a root shell (`setuid(0); setgid(0); system("/bin/bash");`) and compile it locally.
        1. ![[Screenshot_20260515_165816.png]]
            
    3. **Mount:** Mount the vulnerable target share on your local attacking machine (e.g., `sudo mount -t nfs <target_IP>:/tmp /mnt`).
        1. ![[Screenshot_20260515_165840.png]]
            
    4. **Transfer & Escalate:** Copy the compiled binary to the mounted directory and set the SUID bit (`chmod u+s /mnt/shell`).
        
    5. **Execute:** Switch to your low-privileged shell on the target system, run `./shell`, and obtain root access.


## Hijacking Tmux Sessions

- **Concept:** Administrators sometimes leave detached `tmux` (terminal multiplexer) sessions running as root. If the session socket is created with weak permissions or shared group access, it can be hijacked.

- **Exploitation Steps:**
	1. **Identify Sessions:** Search for running tmux processes and identify custom socket paths using `ps aux | grep tmux` (e.g., looking for `-S /shareds`).
		1. ![[Pasted image 20260520112515.png]]
		    
	2. **Check Permissions:** Inspect the socket's ownership and permissions using `ls -la /shareds` (e.g., owned by `root:devs`).
	    
	3. **Verify Groups:** Check if your compromised low-privileged user belongs to the allowed group using the `id` command.
	    
	4. **Hijack:** Attach to the existing session by running `tmux -S /shareds`. You will immediately assume the privileges of the user who started the session (often root).

## References:

