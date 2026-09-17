
2025-03-31 10:30

Tags: #windows  

## Command Prompt (CMD.exe)

- **CMD.exe** is the default ==command-line interpreter== for Windows

- Performing tasks with less resources than GUI


## Accessing CMD

- Two ways:
	- **Local Access** (Direct Physical Access)
		- Win+R, type cmd
		- Navigate to `C:\Windows\System32\cmd.exe`
	- **Remote Access** (Over a Network)
		- Uses protocols like Telnet (insecure), SSH, PsExec, WinRM, or RDP
		- May have security risks

## Basic Usage

- CMD operates in a **request-response format**

- `dir` for listing contents of current directory

- Booting in recovery mode can grant us access to CMD

- But we can replace the sticky key with CMD, then while rebooting -> press Shift 5 times to access CMD with SYSTEM privileges


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1606)