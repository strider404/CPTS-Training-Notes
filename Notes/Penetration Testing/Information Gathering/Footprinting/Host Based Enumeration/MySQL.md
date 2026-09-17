
2025-09-10 15:35

Tags: #footprint  

## MySQL

- **Definition**: MySQL is an **open-source relational database** management system (RDBMS) developed by Oracle that uses Structured Query Language (SQL).

- **Architecture**: It operates on a **client-server model**. The MySQL server stores and manages data, while one or more clients connect to it to retrieve or modify data using SQL queries.

- **Default Port**: MySQL typically runs on TCP **port 3306.**

- **Data Storage**: Data is organized into tables (with rows and columns) within databases. These databases are often stored in files with a `.sql` extension.

- **MariaDB**: A popular open-source RDBMS that was forked from the original MySQL source code.

#### Common Applications

- **Web Applications**: MySQL is ideally suited for dynamic websites due to its efficiency and high response speed.
  
- **LAMP/LEMP Stack**: It is a core component of the popular LAMP (Linux, Apache, MySQL, PHP) and LEMP (Linux, Nginx, MySQL, PHP) web server stacks.
  
- **Content Management Systems (CMS)**: A prime example is WordPress, which uses a MySQL database to store all of its content, including posts, user data, and passwords.


## Security & Configuration
  
- **Default Configuration**
	- Locate in `/etc/mysql/mysql.conf.d/mysqld.cnf`


- **Dangerous Settings**: Several configuration settings are critical for security:
	- `user` and `password`: These can expose credentials in plain text if the configuration file is readable by an unauthorized user.
	  
	- `admin_address`: Defines the IP address for administrative connections.
	  
	- `debug` and `sql_warnings`: If enabled, these can produce verbose error messages that may leak sensitive information about the database structure, potentially aiding in SQL injection attacks.


## Footprinting

- **Nmap** can be used to scan for open MySQL ports, identify versions, and find potential vulnerabilities such as weak or empty passwords.
	- ![[Pasted image 20250910154347.png]]


- **Connection**: The command-line tool `mysql` is used to connect to a MySQL server. The syntax is: `mysql -u <user> -p<password> -h <IP address>`.
	- ![[Pasted image 20250910154421.png]]

- **System Databases**: MySQL includes several default databases for management and metadata, with **information_schema** and **sys** being the **most important**.
	- ![[Pasted image 20250910154523.png]]

- **Basic SQL Commands**:
	- ![[Pasted image 20250910154550.png]]

- [SQL commands](https://www.geeksforgeeks.org/sql/sql-concepts-and-queries/)

## References:
https://academy.hackthebox.com/module/112/section/1238
