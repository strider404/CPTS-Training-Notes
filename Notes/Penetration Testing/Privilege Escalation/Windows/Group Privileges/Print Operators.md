
2026-05-22 10:33

Tags: #escalation 

## Print Operators

- **Group Privileges:** Members of the Print Operators group receive *SeLoadDriverPrivilege*, the ability to manage DC printers, log on locally to a DC, and shut it down.
	- ![[Pasted image 20260522103735.png]]


- **UAC Bypass:** If SeLoadDriverPrivilege is *hidden* in an unelevated context, a UAC bypass (e.g., via the UACMe repository) or an administrative GUI shell is required to expose it.


- **Vulnerability:** The Capcom.sys driver contains **a known flaw allowing any user to execute shellcode with SYSTEM privileges.**


## Standard Exploitation Workflow

- **Preparation:** Download the vulnerable Capcom.sys driver to the target.


- **Tool Compilation:** Update the required includes in EnableSeLoadDriverPrivilege.cpp and compile it via Visual Studio Developer Command Prompt using cl.exe.
	- ![[Pasted image 20260522104545.png]]
	- `cl /DUNICODE /D_UNICODE EnableSeLoadDriverPrivilege.cpp`
	- ![[Pasted image 20260522104455.png]]


- **Registry Configuration:** Add the driver reference to HKCU\System\CurrentControlSet\CAPCOM using an NT Object Path for the ImagePath (e.g., ??\C:\Tools\Capcom.sys) and set the Type to 1.
	- ![[Pasted image 20260522104623.png]]


- **Driver Loading:** Execute the compiled EnableSeLoadDriverPrivilege.exe to enable SeLoadDriverPrivilege and load the driver.
	- ![[Pasted image 20260522104952.png]]


- **Verification:** Confirm the driver is running using Nirsoft's DriverView.exe.
	- ![[Pasted image 20260522105013.png]]


- **Escalation:** Compile and execute ExploitCapcom.exe to launch a shell with SYSTEM privileges.
	- ![[Pasted image 20260522105019.png]]

## Non-GUI Alternative Exploitation

- **Code Modification:** Edit ExploitCapcom.cpp (line 292) before compiling.


- **Payload Replacement:** Swap the default cmd.exe path with a custom msfvenom payload (e.g., a reverse shell executable).
	- ![[Pasted image 20260522105134.png]]


- **Execution:** Set up a listener, run the modified ExploitCapcom.exe, and catch the SYSTEM shell (or use a bind shell if reverse connections are blocked).

## Automation & Cleanup

- **Automated Loading:** Use EoPLoadDriver.exe to combine enabling the privilege, setting the registry keys, and loading the driver into a single command, followed directly by ExploitCapcom.exe.


- **Track Removal:** Always delete the HKCU\System\CurrentControlSet\Capcom registry key after the engagement to clean up.
	- `reg delete HKCU\System\CurrentControlSet\Capcom`


- **Version Limitation:** This specific HKCU registry technique is no longer exploitable on Windows 10 Version 1803 and newer.
## References:

