
2025-03-31 11:00

Tags: #windows #shell #hands-on 

## Getting Help

- `help` command:
	- Using alone: displays a list of built-in commands along with brief descriptions
	- `help <command>`: detailed info of specific command

- When `help` is not supported, try <command> `<command> /?` (e.g., `ipconfig /?`)

- Equivalent to `man` in Bash

- Online sources:
	- [Microsoft Documentation](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
	- [ss64](https://ss64.com/nt/)


## Basic Tips & Tricks

- **Clearing the Screen:** Use `cls` to remove clutter and reset the terminal view.

- **Command History:** CMD keeps a temporary history of commands in the active session. Navigate it using:
	-  **Arrow keys**
	- `doskey /history` command
	-  Function keys like **F3, F5, and F7**
		- **F3** → Retypes the last executed command.
		- **F5** → Similar to the UP arrow
		- **F7** → Opens a **scrollable history menu** of previous commands.
		- **F8** → Complete the command u r typing using previous commands    
		- **F9** → Runs a command from history by specifying its number.
	-  Unlike Bash, CMD does **not** save history between sessions.
		- Bash does save history in ~/.bash_history

- **Exiting a Process:** Ctrl + C

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1607)
