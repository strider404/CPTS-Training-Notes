
2025-02-25 13:48

Tags: #linux 

## System services

- Required during startup

- Perform essential hardware-related task & initialize system components to help the OS perform normally

## User-Installed Services

- Added by users

- Daemons have the letter 'd' at the end of their names (Ex: sshd, systemd)

- Linux adopted ==systemd== as their initialization system (init system) 
	- It's the first processes started when booting, all processes are assigned to a PID (Process ID)
	- Can be seen at /proc/ folder
	- Can have PPID(Parent Process ID), means they were started by another processes

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/73)
