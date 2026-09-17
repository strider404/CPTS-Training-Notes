
2025-02-17 08:57

Tags: #linux 

## Shell

1. Shell provides I/O interface between user and the kernel using commands (==a text - base GUI==)

2. Terminal is ==the interface of the shell interpreter== (can be physical or digital) using CLI
	 The terminal just ==delivers== the command from the user's commands to the shell. The shell is the one that ==processes== and executes the command.  

3. Terminal emulator emulates the functions of terminal (Powershell, Terminatior)
	They have to use physical terminal before, but now we can use it within a graphical environment by the terminal emulator

4. Terminal emulator allows using ==multiple CLIs== to communicate with the shell, each does separated tasks simultaneously

5. BASH (Bourne-again Shell) is the most commonly used shell in Linux

6. **Types**:
    **Reverse Shell**: The compromised system initiates a connection back to the attacker's machine.

    **Bind Shell**: The compromised system opens a port and listens for an incoming connection from the attacker.

    **Web Shell:** Commands are executed through a web browser, often using a malicious script uploaded to the server.



## References:
[Linux Fundamentals](https://academy.hackthebox.com/module/18/section/65)
