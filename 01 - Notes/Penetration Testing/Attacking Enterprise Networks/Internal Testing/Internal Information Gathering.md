
2026-06-11 11:15

Tags: 

## Setting Up the Pivot Tunnel

- To reach the internal `172.16.8.0/23` subnet from the external attack host, a network bridge must be built through the compromised DMZ server (`10.129.203.111`). The lecture covers two distinct methods for establishing this tunnel:

- **Method A: SSH Dynamic Port Forwarding & ProxyChains**
    - A SOCKS proxy is established locally on the attack host using the root private key: `ssh -D 8081 -i dmz01_key root@10.129.203.111`.
        
    - The `/etc/proxychains.conf` file is updated to route traffic through `socks4 127.0.0.1 8081`.
        
    - This configuration allows external tools (like Nmap) to communicate directly with internal targets by prefixing commands with `proxychains`.
    - ![[Pasted image 20260611112156.png]]
        
        
- **Method B: Metasploit Framework (Meterpreter)**
    - An executable payload (`shell.elf`) generated via `msfvenom` is transferred to the target using SCP and executed.
        
    - Once a Meterpreter session is caught using `exploit/multi/handler`, the `post/multi/manage/autoroute` module is executed to automatically configure Metasploit's internal routing table to send traffic destined for `172.16.8.0/23` through the active session.

## Internal Host Discovery

- With routing established, the `172.16.8.0/23` subnet is swept to identify active targets. This can be achieved through:

- **Metasploit:** The `post/multi/gather/ping_sweep` module.
	- ![[Pasted image 20260611112222.png]]

- **Native Shell:** A fast Bash `ping` loop one-liner executed directly on the DMZ host.
	- ![[Pasted image 20260611112243.png]]

- **Discovery Results:** Three internal live hosts are uncovered:
	1. `172.16.8.3`
	    
	2. `172.16.8.20`
	    
	3. `172.16.8.50`

## Host Enumeration & Analyzing "Dead Ends"

- A static Nmap binary is uploaded to the DMZ host to scan the three discovered targets locally, avoiding the latency issues associated with scanning across a SOCKS proxy.
	- ![[Pasted image 20260611112413.png]]

- **Domain Controller (`172.16.8.3`):** Ports 53 (DNS), 88 (Kerberos), 389 (LDAP), and 445 (SMB) are open. An attempt to check for an **SMB NULL Session** via `enum4linux` returns `NT_STATUS_ACCESS_DENIED`, marking it as a dead end for immediate, unauthenticated exploitation.
	- ![[Pasted image 20260611112458.png]]
	    
- **Tomcat Server (`172.16.8.50`):** Port 8080 is running Apache Tomcat 10. A brute-force attack against the Tomcat Manager backend using Metasploit’s `tomcat_mgr_login` module fails to identify valid credentials, ruling it out as an immediate vector.
	- ![[Pasted image 20260611112517.png]]

## The Breakthrough: Pillaging the Development Server (`172.16.8.20`)

- Initial Nmap scans revealed Port 80 (HTTP) and Port 2049 (NFS) open on this host.

- **Web Reconnaissance:** Routing browser traffic through the SOCKS proxy exposes a DotNetNuke (DNN) CMS deployment on port 80. Self-registration is restricted, requiring administrator approval.
	- ![[Pasted image 20260611112724.png]]
	- ![[Pasted image 20260611112732.png]]
	    
- **NFS Misconfiguration:** Running `showmount -e` against the target reveals an anonymous Network File System (NFS) export named `/DEV01` accessible to everyone.
	- ![[Pasted image 20260611112751.png]]
	    
- **Pillaging Actions:** Using root access on the DMZ server, the attacker mounts the remote file share locally (`mount -t nfs 172.16.8.20:/DEV01 /tmp/DEV01`).
	- ![[Pasted image 20260611112812.png]]
	    
- **The Loot:** Inside the mounted `DNN` directory, inspection of the `web.config` file reveals hardcoded plaintext credentials for the site administrator:
    - **Username:** `Administrator`
        
    - **Password:** `D0tn31Nuk3R0ck$$@123`
    - ![[Pasted image 20260611112831.png]]

## Passive Network Traffic Analysis

- As a parallel best-practice step, `tcpdump` is run on the internal interface (`ens192`) of the DMZ host to capture local network traffic. While the resulting packet capture (`.pcap`) does not yield cleartext credentials in this specific instance, it remains a vital strategy during internal penetration assessments to gather environmental data passively.
	- ![[Pasted image 20260611112911.png]]

- **Next Steps:** The assessment will proceed by attempting to use the pillaged administrative credentials to authenticate against the DotNetNuke application on `172.16.8.20` and secure further internal access.


## References:

