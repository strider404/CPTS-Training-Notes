
2025-08-02 16:07

Tags: #bash  

## Debugging

- The `xtrace` (`-x`) Option
	- Running a script with `bash -x <script_name>` enables trace mode.
	  
	- Bash will **print each command and its arguments** to the standard error stream _before_ it is executed.
	  
	- Each trace line is prefixed with a plus sign (`+`), showing the exact command being run after variable expansion and other substitutions.

![[Pasted image 20250802160936.png]]


- The **Verbose** (`-v`) Option
	- Running a script with `bash -v <script_name>` enables verbose mode.
	  
	- Bash will print each line from the script to standard error _as it is read_. This shows the code in its raw form, before any processing.

- Combining Options (`-x` and `-v`)

![[Pasted image 20250802161106.png]]


## References:

https://academy.hackthebox.com/module/21/section/131