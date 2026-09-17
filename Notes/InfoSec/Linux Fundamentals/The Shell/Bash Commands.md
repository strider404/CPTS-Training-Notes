
2025-02-18 10:42

Tags: #bash #linux #hands-on

## Commands

1. **Execute multiple commands:** `(;), (&&), (|)`
	1. (;): separator and executes the commands by ignoring previous commands' results and errors
	2. (&&): run the commands one after the other (if the previous return error the next won't be executed)
	3. (|): make the output of the previous command to the next

2. **Gather information:** `whoami, id, hostname, uname, pwd, ifconfig, ip, netstat, ss, ps, who, env, lsblk, lsusb, lsof, lspci`
	1. id: to see what access a user can have
	2. uname: returns in order: kernel name, hostname, the kernel release, kernel version, machine hardware name, and operating system. Can use the kernel release to check for quick exploits
	3. env: Prints environment | sets or executes environment commands (Environment variables: Dynamic name-values, significantly influence the behavior of the OS)

3. **Navigation:** `pwd, ls, cd`
	4. `ls`: Options: 
		1. -l: to display more infos: Type and permissions, Number of hard links to the file/directory, Owner of the file/directory, Group owner of the file/directory, Size of the file or the number of blocks used to store the directory information, Time, Directory name
		2. -a: list hidden files (with the '.'). Can be used with -l (-la)
		3. -i: display index (inode) numbers
		4. Can add directory in last to list that directory (ls -la /home)
	5. `cd`: 
		1. Can use TAB x2 to autofill
		2. '.' is the directory working in, '..' is the parent directory

4. **Create, Move, and Copy:**  `touch, mkdir, tree, mv, cp`
	1. touch: can add the directory for the file (touch ./Storage/local/user/userinfo.txt)
	2. mkdir: also can add the directory for the file
		1. -p: automatically create parent directories
	3. mv: if 2 variables are file names -> rename; if 1 is name & 1 is directory -> move file

5. **Editing**: `nano, vim` (nvim -> :Tutor for tutoring)

6. **Find:** `which, find, locate`
	4. find: allow filter parameters (name, created newer than, size,... see more in the --help)

7. **Filter:** `more, less, head, tail, sort, grep, cut, tr, column, awk, sed, wc`
	5. more vs less: less is the same with more but has more 
	6. sort: alphabetically
		1. -u: return unique characters
	7. grep: can and should use options, use regex
		1. -v: get ones exclude the characters
		2. -c: count
		3. -i: ignore case
		4. -E: extended regex
		5. -o: show only the part that match
	8. cut: must use options, or error
		6. -d: set delimiter
		7. -f: field ....(add the index of the field number....)
	9. column: use -t to format as a table
	10. awk: `awk '{print $1, $NF}'` to display first and last results, can use $2, $3,... and each field is separate by ' '
	11. sed vs tr: sed use regex so more flexible than tr: `sed 's/bin/HTB/g'` (s: substitute, g: replace all)
	12. wc: 
		1. -l: count lines

8. [**Permission management:**](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FPermission%20Management) `chmod, chown`
	1. chmod: 
		1. `u` - owner, `g` - Group, `o` - others, `a` - All user, +: add permission, -:remove permission (Ex: `chmod a+r shell` )
		2. Quick set: Octal value: `chmod 754 shell`
			1. ![[Pasted image 20250222162046.png]]
	2. chown: `chown <user>:<group> <file/directory>`

9. **User management:** `sudo, su, useradd, userdel, usermod, addgroup, delgroup, passwd`
	1. useradd: 
		1. -m: to create home directory for new user
	2. usermod:
		1. -L: lock user account
	3. su:
		1. -c: execute command as different user

10. [**Package management:**](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FPackage%20Management)`dpkg, apt, aptitude, snap, gem, pip, git`
	1. apt: 
		1. apt-cache: provide info about packages
		2. list: list packages
		3. apt-get install: install if u dont have
		4. apt update && apt dist-upgrade: update

11. [**Service and Process Management:**](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FService%20and%20Process%20Management) `systemctl, ps, journalctl, kill, pkill, pgrep, killall, ping, jobs, bg, fg`
	2. systemctl: 
		1. start: start the service
		2. status: check service status
		3. enable: run the service on startup
		4. list-units: list all units
		5. --type=TYPE: declare the type
	3. kill: some common signals:
		6. ![[Pasted image 20250225134518.png]]

12. [**Web Services:**](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FWeb%20Server%20%26%20Services) `systemctl start apache2, curl, wget, python3`

13. **[Network configuration:](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FNetwork%20Configuration)** `ifconfig, ip, route`
	1. ifconfig might be replaced by ip

14. [Network troubleshooting:](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FNetwork%20Configuration) `ping, traceroute, netstat`
	2. ping: test connectivity between 2 devices, measure the time for the packets to be delivered
	3. traceroute: trace the route (path) which the packets take to reach a remote host
	4. netstat: display active network connections and their associated ports

15. **Shortcuts**:
	1. clear: clear the terminal or use Ctrl + L to just scroll to new line
	2. Ctrl + U: delete the line from the cursor back the the head
	3. TAB: auto complete
	4. Ctrl + W: delete the word the cursor is in
	5. Ctrl + R: search the previous command

## References:

