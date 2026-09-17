
2025-03-08 21:50

Tags: #linux  

## System Logs

- System logs: set of files that contain info about system activity, application behavior, and security events
	- -> used for monitoring, troubleshooting, indentifying vulnerabilities,...

- Key system logs:
	- Kernel Logs
	- System Logs
	- Authentication Logs
	- Application Logs
	- Security Logs

| **Log Type**            | **Default File Location**                                                                             | **Description**                                                                                                                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Kernel Logs**         | `/var/log/kern.log`                                                                                   | Contains ==kernel events== including hardware drivers, system calls, and crashes. Useful for identifying vulnerable drivers, resource issues, and suspicious kernel activities.       |
| **System Logs**         | `/var/log/syslog`                                                                                     | Records ==system-level events== such as service starts/stops, login attempts, and reboots. Helps detect abnormal behavior and potential vulnerabilities affecting system performance. |
| **Authentication Logs** | `/var/log/auth.log`                                                                                   | Focuses on ==user authentication attempts== (both successful and failed). Crucial for tracking access control and detecting unauthorized access.                                      |
| **Application Logs**    | Varies by application (e.g., Apache: `/var/log/apache2/error.log`; MySQL: `/var/log/mysql/error.log`) | Captures events specific to ==applications==. Includes access and audit logs, which help identify misconfigurations and unauthorized data access in targeted services.                |
| **Security Logs**       | Varies by tool (e.g., Fail2ban: `/var/log/fail2ban.log`; UFW: `/var/log/ufw.log`)                     | Logs ==security-related events== like failed login attempts, unexpected network traffic, and unauthorized changes. Essential for pinpointing security threats and breaches.           |

- Access logs & audit logs (part of application logs):
	- Access logs: track user and process activities such as login attempts, file accesses, and network connections
	- Audit logs record changes to system configuration or files

- Some application's log file directories can be view in the link below

- Tools like tail, grep, sed often used

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2100)