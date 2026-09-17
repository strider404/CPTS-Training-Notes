
2026-05-19 10:17

Tags: 

## Python Library Hijacking

- Python relies heavily on external and standard libraries (like NumPy and Pandas) to expand functionality and save developers time. However, the way Python handles module imports can be actively exploited for **Privilege Escalation** if file permissions or environment variables are misconfigured within a system.

## The Three Attack Vectors

- There are three primary vulnerabilities that allow an attacker to hijack a Python library and execute malicious code:

|**Attack Vector**|**Underlying Vulnerability**|**Exploitation Strategy**|
|---|---|---|
|**Wrong Write Permissions**|Global write access on a legitimate module file.|Injecting malicious code directly into the module used by a privileged script.|
|**Library Path Precedence**|Write access to a directory high in Python's search priority.|Planting a fake module with the target name in a higher-priority directory.|
|**PYTHONPATH Variable**|`sudo` privileges with the `SETENV:` flag enabled.|Modifying `PYTHONPATH` to prioritize an attacker-controlled directory.|

## Wrong Write Permissions

- This vulnerability occurs when a script running with **elevated privileges** (such as one with a SUID bit set) imports a module that is accidentally left **globally writable.**


- An attacker can directly **edit** the legitimate module's file to include malicious code, such as importing the `os` module and adding a system command like `os.system('id')` or a reverse shell.


- When the privileged script runs and calls the hijacked function, it automatically executes the injected payload as root.

![[Pasted image 20260519163720.png]]
![[Pasted image 20260519163734.png]]
![[Pasted image 20260519163744.png]]
![[Pasted image 20260519163807.png]]
![[Pasted image 20260519163814.png]]

## Library Path

- Python searches for imported modules in a strict, **priority-based hierarchical order.**


- If an attacker finds a globally *writable directory* that sits *higher on this priority* list than the directory housing the legitimate module, they can create a malicious script using the exact same module name (e.g., `psutil.py`).


- Because Python accesses the first hit it finds, it will import and execute the attacker's fake file before ever reaching the real module.
![[Pasted image 20260519163626.png]]
![[Pasted image 20260519163532.png]]
![[Pasted image 20260519163541.png]]
![[Pasted image 20260519163553.png]]
![[Pasted image 20260519163603.png]]

## PYTHONPATH Environment Variable

- The `PYTHONPATH` variable dictates the directories Python checks for modules.


- If a user is allowed to run Python via `sudo` and their permissions include the `SETENV:` directive, they can bypass normal restrictions and define environment variables prior to calling the binary.


- By running a command like `sudo PYTHONPATH=/tmp/ python3 script.py`, the attacker forces Python to check the `/tmp` directory first, allowing a malicious module planted there to be executed under the context of root.

![[Pasted image 20260519163434.png]]

![[Pasted image 20260519163441.png]]
## References:

