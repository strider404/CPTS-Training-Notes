
2025-07-25 11:55

Tags: #web  

## Broken Authentication & Broken Access Control

- **Description:** These are vulnerabilities related to user identity and permissions.
	- **Broken Authentication** allows an attacker to *bypass login functions*, potentially gaining access without credentials or escalating privileges from a normal user to an administrator.
	  
	- **Broken Access Control** allows users to *access resources and functionalities they are not authorized for,* such as a standard user accessing an admin panel.

- **Example:** Bypassing a login form by injecting a SQL statement like `' or 0=0 #` into the username/email field.

## Malicious File Upload

- **Description:** This vulnerability occurs when a web application *allows users to upload files but fails to properly validate the file's type, content, or extension.*

- **Impact:** An attacker can upload a malicious script (e.g., a PHP web shell) to the server, enabling remote command execution and potentially a full system compromise.

- **Example:** Bypassing extension filters by using a double extension, such as `shell.php.jpg`.

## Command Injection

-  **Description:** This flaw arises when *an application passes unsanitized user-supplied data as input* to a system shell command.

- **Impact:** Attackers can *inject arbitrary operating system (OS) commands* to be executed on the back-end server, leading to unauthorized access and control.

- **Example:** Injecting a command by appending `| <COMMAND>` to user input that is expected to be a value like an IP address.

## SQL Injection (SQLi)

- **Description:** Similar to command injection, SQLi occurs when an *application incorporates unsanitized user input into a SQL query.*

- **Impact:** Attackers can manipulate the query to bypass authentication, exfiltrate sensitive data from the database, modify database content, or even take control of the database server.

- **Example:** A login form vulnerable to SQLi can be bypassed by injecting a query that always returns a `true` condition.


## References:

https://academy.hackthebox.com/module/75/section/764