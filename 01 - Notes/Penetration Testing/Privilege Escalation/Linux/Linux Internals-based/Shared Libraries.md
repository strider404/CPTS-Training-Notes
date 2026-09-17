
2026-05-18 16:31

Tags: #escalation  

## Shared Libraries

- **Purpose:** Pre-compiled code used across multiple Linux programs to prevent code duplication.


- **Static Libraries (`.a`):** Baked directly into the program *during compilation* and cannot be altered dynamically.


- **Dynamic Libraries (`.so`):** Loaded at *runtime* and can be modified to influence the calling program's execution.


- **Location Specification:** Defined via compiler flags (`-rpath`, `-rpath-link`), environment variables (`LD_RUN_PATH`, `LD_LIBRARY_PATH`), default directories (`/lib`, `/usr/lib`), or the `/etc/ld.so.conf` file.


- **LD_PRELOAD Variable:** An environment variable that *loads a specified library before executing a binary*, forcing the program to prioritize its functions over default ones.


- **Inspection Tool:** The `ldd` command (e.g., `ldd /bin/ls`) reveals all shared objects required by a specific binary.
	- ![[Screenshot_20260518_163748.png]]

## LD_PRELOAD Privilege Escalation

- **Prerequisite:** Sudo privileges on a system where the `/etc/sudoers` configuration explicitly includes `env_keep+=LD_PRELOAD`.
	- ![[Screenshot_20260518_163813.png]]


- **Malicious Payload:** A custom C script utilizing the `_init()` function, which automatically executes when the library is loaded.
	- ![[Screenshot_20260518_163840.png]]


- **Payload Actions:** The C script must unset `LD_PRELOAD` (to prevent execution loops in subsequent commands), elevate privileges with `setgid(0)` and `setuid(0)`, and spawn a shell using `system("/bin/bash")`.


- **Compilation:** The code is compiled into a shared object using the command: `gcc -fPIC -shared -o root.so root.c -nostartfiles`.
	- **`-fPIC` (Position Independent Code)**
		- **Function:** Instructs the compiler to generate machine code that executes correctly regardless of where it is placed in memory.
	- **`-shared`**
		- **Function:** Directs the linker to produce a shared object (`.so` file) rather than a standard, standalone executable binary.


- **Exploitation:** The payload is triggered by running the allowed sudo command with the malicious library prepended: `sudo LD_PRELOAD=/path/to/root.so <allowed_sudo_command>`.
	- ![[Screenshot_20260518_163926.png]]


- **Outcome:** The execution flow of the highly privileged command is hijacked, resulting in a root shell.
## References:

https://academy.hackthebox.com/app/module/51/section/475