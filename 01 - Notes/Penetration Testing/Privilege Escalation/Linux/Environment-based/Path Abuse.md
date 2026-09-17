
2026-05-12 09:23

Tags: #escalation  

## Path Abuse

- **Definition:** `PATH` is an environment variable that *stores a list of directories containing executable files.*
	- ![[Pasted image 20260512092527.png]]


- **Purpose:** It allows users to *run commands* (like `cat` or `ls`) *without typing their full absolute paths* (like `/bin/cat`).


- **Visibility:** You can check a system's PATH configuration by running `echo $PATH` or `env | grep PATH`.


- **Global Execution:** If you place a custom script or program into any directory listed in the `PATH`, you can execute it from anywhere on the system.

## The Path Abuse Mechanism

- **Adding the Current Directory:** A user can add their current working directory (`.`) to the beginning of their PATH using the command `PATH=.:$PATH` followed by `export PATH`.
	- ![[Pasted image 20260512092550.png]]


- **Execution Order:** The system searches directories in the exact order they appear in the `PATH` variable. By placing `.` at the very beginning, the system will *check the current directory* for an executable _before_ checking standard system directories like `/bin` or `/usr/bin`.


- **The Exploit:** An attacker can create a malicious script and name it after a common command (e.g., `ls`). Make it executable using `chmod +x ls`.


- **The Result:** When the user types `ls`, the system finds the attacker's script in the current directory first and executes it, effectively hijacking the command and bypassing the legitimate binary located at `/bin/ls`.
	- ![[Pasted image 20260512092628.png]]
## References:

