
2025-09-11 09:47

Tags: #footprint  

## MSSQL

- **Definition**: MSSQL is a *closed-source*, SQL-based *relational database* management system (RDBMS) developed by Microsoft.
  
- **Port 1443**
  
- **Platform**: It was initially designed for Windows and integrates strongly with the .NET framework, though versions for Linux and macOS are now available.


#### Clients & Tools

- **SQL Server Management Studio (SSMS)**: The primary client for managing MSSQL, which can be installed on the server or a separate system. Saved credentials within SSMS can pose a security risk.
	- ![[Pasted image 20250911095318.png]]

- **Pentesting Tools**: For penetration testers, Impacket's `mssqlclient.py` is a highly useful command-line client that is often included in security-focused Linux distributions.
	- ![[Pasted image 20250911095657.png]]


#### Default Databases

- MSSQL includes several default system databases upon installation:
	- **master**: Contains all system-level information for the SQL server instance.
	  
	- **model**: Acts as a template for all newly created databases.
	  
	- **msdb**: Used by the SQL Server Agent for scheduling alerts and jobs.
	  
	- **tempdb**: Stores temporary tables and objects.
	  
	- **resource**: A read-only database containing system objects.


## Configuration & Security

- **Default Service Account**: The SQL service typically runs under the `NT SERVICE\MSSQLSERVER` account.

- **Connect from client-side**:
	- ![[Pasted image 20250911100103.png]]

- **Authentication**: It often uses "**Windows Authentication**," where the operating system (via the local SAM database or Active Directory) manages login requests. This can be exploited for lateral movement if an account is compromised.

- **Common Misconfigurations (Vulnerabilities)**:
	- Client connections are **not encrypted by default**.
	  
	- Use of weak, self-signed certificates that can be spoofed.
	  
	- Enabled named pipes.
	  
	- Weak or default passwords for the **`sa` (system administrator)** account, which administrators may forget to disable.


## Footprinting

- The service typically listens on **TCP port 1433**.

- Tools like **Nmap** (with its `ms-sql-*` scripts) and **Metasploit** (using the `mssql_ping` auxiliary scanner) can be used to *gather information* such as the hostname, instance name, software version, and enabled protocols.
	- **Nmap**:
		- `sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248`
		- Or just `ms-sql-*`
	- **msf6**:
		- ![[Pasted image 20250911100437.png]]


- **If valid credentials are obtained,** an attacker can connect remotely using tools like `mssqlclient.py` to interact with the databases using T-SQL commands.
	- Need to create an python environment first `python3 -m venv .venv`
	- Activate it with `source .venv/bin/activate`
	- Install `impacket` packet if needed `pip install impacket`
	- ![[Pasted image 20250911100527.png]]

## References:

https://academy.hackthebox.com/module/112/section/1246