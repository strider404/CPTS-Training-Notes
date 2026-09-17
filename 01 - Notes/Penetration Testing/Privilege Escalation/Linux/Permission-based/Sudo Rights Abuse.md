
2026-05-13 15:46

Tags: #escalation  

## Sudo Rights Abuse

- **Purpose:** `sudo` permits users to execute commands in the context of root (or another user) based on the `/etc/sudoers` configuration.


- **Reconnaissance:** Run `sudo -l` to check your current privileges upon landing on a system.


- **Target:** Look specifically for `NOPASSWD` entries, which allow command execution without requiring the user's password.
	- ![[Pasted image 20260513154730.png]]

## Vulnerability & Exploitation (Example: `tcpdump`)

- **The Flaw:** Loosely defined command permissions (e.g., `(ALL) NOPASSWD: /usr/sbin/tcpdump`) can be leveraged to execute unintended programs.


- **The Exploit Vector:** `tcpdump` includes a `-z postrotate-command` flag, which *executes a specified file/script after a capture file is closed.*


- **Attack Steps:**
    1. Create a malicious payload, such as a reverse shell script (e.g., `/tmp/.test`).
        1. ![[Pasted image 20260513154918.png]]
            
    2. Set up a Netcat listener on the attacking machine.
        
    3. Execute `tcpdump` with the postrotate flag pointing to the payload: `sudo /usr/sbin/tcpdump -ln -i eth0 -w /dev/null -W 1 -G 1 -z /tmp/.test -Z root`
        1. ![[Pasted image 20260513154935.png]]


- **Result:** The script executes as root, spawning a privileged reverse shell.
	- ![[Pasted image 20260513154946.png]]


## Mitigation & Best Practices

- **System Defenses:** Modern distributions use AppArmor to restrict the commands that can be executed via the `postrotate-command`, mitigating this specific vector.


- **Absolute Paths:** Always specify the absolute path for binaries in `/etc/sudoers` (e.g., `/bin/cat` instead of `cat`) to prevent attackers from leveraging PATH abuse.


- **Principle of Least Privilege:** Grant `sudo` rights strictly on a need-to-have basis, limiting the number of allowed commands to reduce the attack surface.

## References:

