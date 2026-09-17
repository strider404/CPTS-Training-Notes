
2025-04-02 10:38

Tags: #windows #shell #hands-on

## Listing A Directory

- `dir`: display the contents of the current directory.
	- `/A: <attribute>`: display directories or files with that attribute (`dir /A:R`)

## Finding Our Place

- `cd` or `chdir`: determine the current working directory.
	- cd alone: gives us our current working directory

## Moving Around Using CD/CHDIR

- `cd` with arguments (path): move to that path
	- Absolute path (full path)
	- Relative path: 
		- `.` for current directory
		- `..` for parent directory

- Relative path can be used in reverse: `cd ..\..\..\` (back to the root)


## Exploring the File System

- `tree` command: List directories and subdirectories in hierarchical view
	- Can be used with `/F` to lists ==both directories and files==

## Interesting Directories

- Directories to drop some "sauce":

| **Name**              | **Location**                         | **Description**                                                                                                                                                      |
| --------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `%SYSTEMROOT%\Temp`   | `C:\Windows\Temp`                    | Global directory containing temporary system files. **All users have full read, write, and execute permissions.** Useful for dropping files as a low-privilege user. |
| `%TEMP%`              | `C:\Users\<user>\AppData\Local\Temp` | User-specific temp directory. Only accessible by the associated user. Useful when an attacker **has access to a local/domain user account.**                         |
| `%PUBLIC%`            | `C:\Users\Public`                    | Public directory accessible to all interactive logon accounts. **Allows full read, write, modify, and execute access.** Less monitored than `C:\Windows\Temp`.       |
| `%ProgramFiles%`      | `C:\Program Files`                   | Contains installed **64-bit** applications. Useful for identifying software on the system.                                                                           |
| `%ProgramFiles(x86)%` | `C:\Program Files (x86)`             | Contains installed **32-bit** applications. Useful for identifying software on the system.                                                                           |




## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1609)