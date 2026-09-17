
2025-03-21 10:46

Tags: #windows  

## Windows Sessions

 - Windows logon sessions have 2 types:
	 - Interactive logon: requires user authentication (direct system login, runas command, Remote Desktop)
	 - Non-interactive logon: does not require user credentials and is used by Windows for running services and applications automatically

- Three types of non-interactive accounts:
	- **Local System Account (NT AUTHORITY\SYSTEM)** – ==The most powerful==, used for OS-level tasks and service management
	- **Local Service Account (NT AUTHORITY\LocalService)** – A ==restricted== account with privileges similar to a local user, used for running some services.
	- **Network Service Account (NT AUTHORITY\NetworkService)** – Similar to a ==domain== user, allows authenticated network sessions.



## References:

[Windows Fundamentals](https://academy.hackthebox.com/module/49/section/459)