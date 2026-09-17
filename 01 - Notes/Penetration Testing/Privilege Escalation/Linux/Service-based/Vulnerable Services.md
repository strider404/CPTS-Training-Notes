
2026-05-14 15:15

Tags: #escalation  

## Vulnerable Services

- Many installed system services contain **flaws** that can be exploited for privilege escalation.


- **GNU Screen version 4.5.0** suffers from a specific privilege escalation vulnerability due to a missing permissions check when handling log files.


- This flaw allows unprivileged users to create or truncate files owned by `root` in any directory.

## Identification

- Verify the installed version by executing: `screen -v`.
	- ![[Pasted image 20260514153728.png]]

## Exploitation Mechanism (The `ld.so.preload` Abuse)

- **Payload Compilation:** The exploit script writes and compiles two C programs into the `/tmp` directory:
    1. `libhax.so`: A malicious shared library. When loaded, it executes a function that **changes the ownership of the target shell to root,** sets the SUID bit (`04755`), and deletes the `ld.so.preload` file to clean up its tracks.
    2. ![[Pasted image 20260514153818.png]]
        
    3. `rootshell`: A simple C executable that sets the user ID to `0` (root) and spawns a `/bin/sh` shell.
    4. ![[Pasted image 20260514153755.png]]


- **File Overwrite:** The script abuses the vulnerable log-writing feature of Screen using `screen -D -m -L ld.so.preload echo -ne "\x0a/tmp/libhax.so"`. This forces the SUID `screen` binary to append the path of the malicious library into `/etc/ld.so.preload`.
	- ![[Pasted image 20260514153907.png]]


- **Triggering the Exploit:** The script runs `screen -ls`. Because `screen` is a SUID binary, executing it forces the system to load the contents of `/etc/ld.so.preload`, which in turn executes the `libhax.so` payload with root privileges.


- **Gaining Access:** With the SUID bit now set on `/tmp/rootshell` by the triggered library, the attacker simply executes `/tmp/rootshell` to drop into a root shell (`uid=0`).
## References:

