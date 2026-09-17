
2026-05-18 16:50

Tags: #escalation  

## Shared Object Hijacking

- **Vulnerability Identification**
    - Identify a target SETUID binary (e.g., using `ls -la`).
        - ![[Screenshot_20260518_165200.png]]
          
    - Use the `ldd` utility against the binary to map its shared object dependencies and locate any non-standard libraries.
        - ![[Screenshot_20260518_165229.png]]
          
    - Use `readelf -d <binary> | grep PATH` to inspect the `RUNPATH` configuration. This setting dictates preferred directories for loading libraries.
        - ![[Screenshot_20260518_165251.png]]
          
    - Verify the permissions of the `RUNPATH` directory (e.g., `ls -la /development/`). A world-writable directory (`drwxrwxrwx`) indicates a hijackable path.
        - ![[Pasted image 20260519093302.png]]


- **Information Gathering**
    - Determine the specific function the binary expects from the custom library.
        - ![[Pasted image 20260519093336.png]]
            
    - A quick method is to copy an incompatible but valid library (like `libc.so.6`) into the writable `RUNPATH` directory with the expected library name.
        - ![[Pasted image 20260519093346.png]]
            
    - Execute the binary; the resulting error will reveal the missing function's name (e.g., `symbol lookup error: ./payroll: undefined symbol: dbquery`).
        - ![[Pasted image 20260519093403.png]]


- **Exploitation Process**
	- Write a malicious C script containing a function matching the missing symbol name (e.g., `void dbquery()`).
		- ![[Pasted image 20260519093528.png]]
		    
	- Inside this function, include privilege escalation commands such as `setuid(0);` and `system("/bin/sh -p");`.
	    
	- Compile the malicious script into a shared object using `gcc` and place it in the writable `RUNPATH` directory: `gcc src.c -fPIC -shared -o /development/libshared.so`.
		- ![[Pasted image 20260519093540.png]]
		    
	- Execute the SETUID binary. Because the binary trusts the `RUNPATH` directory first, it will load the malicious library, trigger the function, and spawn a root shell.
		- ![[Pasted image 20260519093548.png]]
## References:

