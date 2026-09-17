
2025-03-17 10:57

Tags: #windows 

## Windows Services

- **Windows Services**: ==background processes== automatically start when the system is booted up & work even when the user logoff

- Manage through Service Control Manager (SCM), can be accessed using services.msc or sc.exe (Get-Service in PowerShell)

- Service **statuses**: 
	- Running
	- Stopped
	- Paused

- Service **start options**:
	- Manually
	- Automatically
	- With a delay

- Service **categories**:
	- Local Services
	- Network Services
	- System Services

- Some services (smss.exe, csrss.exe, wininit.exe, lsass.exe, winlogon.exe, svchost.exe,...) are critical services, cannot be updated or stopped without a system reboot (see more in the link)


## Windows Process

- **Processes**: run in the background, started by the OS or applications

- **Process** = Services + apps' process

- Apps' process can be terminated


## Local Security Authority Subsystem Service (LSASS)

- **lsass.exe** response for verifying user logon attempts and generating access tokens.

- Manages password changes and logs security events (logon/logoff).

- Is a ==high-value target==, because several tools exist to extract both cleartext and hashed credentials stored in memory by this process.


## Sysinternals Tools

- Sysinternals Tools suite is set of portable Windows applications

- Available from Microsoft or via an online share (\live.sysinternals.com\tools) (ProcDump, Process Explorer,...)

- Valuable for penetration testers to identify process behaviors, privilege escalation paths, and facilitate lateral movement.


## Task Manager

- Task manager used to monitoring running processes, system performance, services, startup applications, and user sessions

- Tabs:

| Tab             | Description                                                                                                                                                                                                                                                          |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Processes tab   | Shows a list of ==running applications and background processes== along with the ==CPU, memory, disk, network, and power usage== for each.                                                                                                                           |
| Performance tab | Shows graphs and data such as ==CPU utilization, system uptime, memory usage, disk and, networking, and GPU usage==. We can also open the `Resource Monitor`, which gives us a much more in-depth view of the current CPU, Memory, Disk, and Network resource usage. |
| App history tab | Shows ==resource usage for the current user account== for each application for a period of time.                                                                                                                                                                     |
| Startup tab     | Shows ==which applications are configured to start at boot== as well as the impact on the startup process.                                                                                                                                                           |
| Users tab       | Shows ==logged in users== and the processes/resource usage associated with their session.                                                                                                                                                                            |
| Details tab     | Shows the name, process ID (PID), status, associated username, CPU, and memory usage for each ==running application.==                                                                                                                                               |
| Services tab    | Shows the name, PID, description, and status of each ==installed service==. The Services add-in can be accessed from this tab as well.                                                                                                                               |

## Process Explorer

- Process Explorer: part of the Sysinternals suite, offers an advanced view of running processes including loaded handles, DLLs, and memory-mapped files

- Useful for analyzing parent-child process relationships and troubleshooting issues such as orphaned processes

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/457)