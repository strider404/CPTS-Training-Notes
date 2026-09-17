
2026-05-21 09:29

Tags: #escalation  

## Communication with Processes

- **Privilege Escalation Vector:** Non-administrator processes (e.g., web servers like IIS or XAMPP) often hold the **SeImpersonate** privilege.


- **Potato Attacks:** By placing a shell in these services, attackers can *leverage the SeImpersonate token to escalate to SYSTEM* using exploits like Rogue, Juicy, or Lonely Potato.


- **Access Tokens:** Windows uses these to define the security context (identity and permissions) of a process or thread. A copy is presented to verify privilege levels during process interaction.

## Enumerating Network Services

- **Local Sockets:** Processes frequently communicate over network sockets.


- **Discovery:** The `netstat -ano` command reveals active TCP and UDP connections and their associated PIDs.


- **High-Value Targets:** Services listening exclusively on loopback addresses (`127.0.0.1` and `::1`). These often lack strong authentication under the assumption they are internally isolated.


- **Exploitable Examples:**
    - **FileZilla Server:** The local administrative interface on port 14147 can be abused to extract FTP passwords or create high-privileged FTP shares.
        
    - **Splunk Universal Forwarder:** Default installations historically ran as SYSTEM without authentication, allowing arbitrary code execution via application deployment.
        
    - **Erlang Port (25672):** Designed for distributed computing, relying on a secret "cookie" to join the cluster. Applications (RabbitMQ, CouchDB, SolarWinds) often use weak default cookies (e.g., `rabbit`) or expose them in readable config files.


## Named Pipes

- **Definition:** Shared memory files used for **inter-process communication (IPC).** They operate on a client-server model and are cleared out after being read.


- **Evasion & C2:** Frameworks like *Cobalt Strike* rely on named pipes to safely execute commands without risking the main beacon process, often renaming them to masquerade as legitimate software (e.g., `mojo` for Chrome).


- **Discovery Tools:**
    - Sysinternals: `pipelist.exe /accepteula`
        - ![[Pasted image 20260521093528.png]]
            
    - PowerShell: `gci \\.\pipe\`
        - ![[Pasted image 20260521093539.png]]


- **Permission Checks:** Sysinternals `accesschk.exe` is used to inspect Discretionary Access Control Lists (DACLs) to see who can read, write, or execute a pipe.
    - _Example:_ `accesschk.exe /accepteula \\.\Pipe\lsass -v`
        - ![[Pasted image 20260521093610.png]]


- **Attack Example (WindscribeService):** Searching for globally writable pipes (`accesschk.exe -w \pipe\* -v`) revealed the Windscribe pipe granted `FILE_ALL_ACCESS` to the **Everyone** group, granting any authenticated user an avenue to escalate to SYSTEM.
	- ![[Pasted image 20260521093630.png]]
## References:

