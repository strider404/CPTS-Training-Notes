
2025-04-02 16:13

Tags: #windows #shell #hands-on

## Directories

- `cd` (change directory), `dir` (list files), and `tree` (display directory structure).

## Create A New Directory

- `md <dir>` or `mkdir <dir>`: create new folder in current directory

## Delete Directories

- `rd <dir>` or `rmdir <dir>`: delete a directory
	- Use with `/S` to remove all files and folders in it


## Modifying

- `move <source> <destination>`: move file or directory to new location
	- e.g., `move example C:\Users\htb\Documents\example`


- `xcopy <source> <destination> <option>`: Copies directories and files
	- /E: including all subdirectories and files in it
	- /K: don't reset file attribute (read-only, hidden), if not used it will be reset
	- e.g., `xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E`

- `robocopy <option> <source> <destination>`: like xcopy but more capability, retains timestamps, ownership, ACLs, and file attributes
	- `/E`: Copies all directories, including empty ones
	- `/B`: Uses backup mode (requires special user permissions)
	- `/L`: Runs the command in "what-if" mode (only lists the files without actually copying them)
	- `/MIR`: **Mirrors** the directory, making the destination identical to the source (deletes extra files in the destination)
	- `/A-:SH`: Removes the **System (S)** and **Hidden (H)** attributes from copied files
	- e.g., `robocopy /E /MIR /A-:SH C:\Users\htb\Desktop\notes\ C:\Users\htb\Documents\Backup\Files-to-exfil\`


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1610)