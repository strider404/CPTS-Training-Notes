
2026-05-19 18:13

Tags: #escalation  

## Polkit

- **PolicyKit (polkit)** is an *authorization service* in Linux operating systems that controls **how user applications and system components communicate with one another based on defined privileges**. It allows fine-grained access control, determining whether an action should be allowed, blocked, or require administrative authentication.

## Polkit Architecture & Core Components

- Polkit determines authorizations using **two main groups of files:**
	- **Actions/Policies:** Located in `/usr/share/polkit-1/actions`
	    
	- **Rules:** Located in `/usr/share/polkit-1/rules.d`


- Custom local authority rules can also be added via `.pkla` files in `/etc/polkit-1/localauthority/50-local.d`.

## Primary Polkit Programs

|**Tool**|**Purpose**|**Significance to Attackers**|
|---|---|---|
|**`pkexec`**|Runs a program with the privileges of another user or root (similar to `sudo`).|**High** - Direct target for privilege escalation.|
|**`pkaction`**|Displays available actions and rules.|Low - Used for system enumeration.|
|**`pkcheck`**|Checks if a specific process is authorized for a given action.|Low - Used for authorization checks.|

## The Pwnkit Vulnerability (CVE-2021-4034)

- The most notable vulnerability associated with Polkit is **CVE-2021-4034**, universally known as **Pwnkit**.
	- **The Flaw:** Pwnkit is a memory corruption vulnerability found within the `pkexec` utility. Similar to other major Linux vulnerabilities, it existed undetected in the codebase for over a decade before being disclosed and patched in late 2021/early 2022.
	    
	- **Exploitation Strategy:** Because `pkexec` inherently runs with elevated capabilities to allow users to execute commands as root, exploiting its internal memory corruption completely bypasses authorization checks.
	    
	- **Execution:** An attacker leverages a public Proof-of-Concept (PoC) script written in C. By cloning the repository and compiling it locally (`gcc cve-2021-4034-poc.c -o poc`), running the resulting binary instantly grants the attacker an interactive root shell (`uid=0`).
	- `git clone https://github.com/arthepsy/CVE-2021-4034.git`
## References:

