
2025-09-11 14:11

Tags: #footprint  

## Oracle TNS

- **Definition:** Oracle TNS is a *communication protocol* within the Oracle Net Services suite that enables communication *between Oracle databases and client applications* across various network protocols like TCP/IP.

- **Purpose:** It is primarily used for managing large, complex databases and serves several key functions:
    - Name resolution
      
    - Connection management
      
    - Load balancing
      
    - Security through built-in encryption (supporting SSL/TLS)


- **Default Port:** The TNS listener typically uses TCP port **1521** by default.

## Configuration

- `tnsnames.ora`: A **client-side** file that **maps service names to network addresses** and connection data, allowing clients to find and connect to the database. It is usually located in `$ORACLE_HOME/network/admin`.
- ![[Pasted image 20250911142033.png]]


- `listener.ora`: A **server-side** file that **defines the properties for the listener process**, specifying which services to listen for and how to handle incoming requests.
- ![[Pasted image 20250911142623.png]]

- **Default Security:**
	- Older Oracle versions (e.g., Oracle 9i) had default passwords like `CHANGE_ON_INSTALL`.
	  
	- Remote management was enabled by default in versions 8i/9i but disabled in 10g/11g.


## Security and Enumeration

- **System Identifier (SID):** A unique name that identifies a specific database instance. It is crucial for establishing a connection.

- **Enumeration Tools:** Tools can be used to gather information about and identify vulnerabilities in an Oracle TNS setup.
	- **Nmap:** Used for port scanning (`-p1521`) and **brute-forcing SIDs** (`oracle-sid-brute` script).
	- ![[Pasted image 20250911153322.png]]
	  
	- **ODAT (Oracle Database Attacking Tool):** A Python-based tool for comprehensive enumeration and exploitation, capable of *guessing SIDs, usernames, and passwords.*
	- ![[Pasted image 20250911153335.png]]


- **Connection and Interaction:**
	- **SQLPlus:** A command-line tool used to connect to and *interact with the Oracle database* after valid credentials have been obtained.
	  
	- The command format is typically `sqlplus username/password@HOST/SID`.
	- ![[Pasted image 20250911153502.png]]


## Post-Exploitation Techniques

- **Privilege Escalation:** After gaining initial access (e.g., with a user like `scott`), an attacker might attempt to connect with **higher privileges**, such as `as sysdba`, if the user has been granted them.
	- ![[Pasted image 20250911154049.png]]


- **Information Gathering:** Once connected, one can execute SQL queries to list tables, view user privileges, and **extract sensitive data** like password hashes from system tables (e.g., `sys.user$`).
	- Remember the `$` in the end
	- ![[Pasted image 20250911154105.png]]


- **File Upload:** If the database server is also running a web server, it may be possible to upload files (like a web shell) to the **web root directory** (e.g., `/var/www/html` in Linux or `C:\inetpub\wwwroot` in Windows) using database functionalities.
## References:

https://academy.hackthebox.com/module/112/section/2117