
2026-05-12 14:30

Tags: #escalation  

## Escaping Restricted Shells

- **Definition:** Shell environments that *intentionally limit a user's ability* to execute specific commands, change directories, or modify settings.


- **Purpose:** Used by administrators to *secure systems and networks* by preventing accidental or malicious damage while still granting users necessary access.


- **Use Case:** Assigning different restriction levels based on user roles (e.g., strict limits for external partners, moderate limits for contractors, flexible limits for specific employees).


## Common Types of Restricted Shells

- **RBASH (Restricted Bourne Shell):** Restricts changing directories, setting/modifying environment variables, and executing commands in other directories.
    
- **RKSH (Restricted Korn Shell):** Restricts executing commands in other directories, creating/modifying shell functions, and altering the shell environment.
    
- **RZSH (Restricted Z Shell):** Restricts running shell scripts, defining aliases, and modifying the shell environment.

## Common Escaping Techniques

- **Command Injection:** Injecting hidden commands into the arguments of an allowed command.
    - _Example:_ Running `ls -l 'pwd'` allows the restricted user to see their working directory because pwd is evaluated as an argument for the permitted ls command.


- **Command Substitution:** Leveraging the shell's substitution syntax (like backticks) to execute a restricted command within an allowed operation.


- **Command Chaining:** Using shell metacharacters like a semicolon (`;`) or a vertical pipe (`|`) to run multiple commands on a single line, allowing an unrestricted command to slip past following an allowed one.


- **Environment Variables:** Manipulating environment variables (like execution paths) to point the shell toward directories or commands that bypass the restrictions.

- **Shell Functions:** Defining and calling custom shell functions that execute unrestricted commands, bypassing blocks that apply to standard command-line input.

- **Escape from outside**
	- `ssh htb-user@10.129.112.152 -t "bash --noprofile"`

## References:

