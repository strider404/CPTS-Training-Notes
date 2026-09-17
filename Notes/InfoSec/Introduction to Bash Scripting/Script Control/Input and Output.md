
2025-08-02 11:02

Tags: #bash  

## Input

- Scripts **can be designed to pause and wait** for manual user instructions to determine subsequent actions.

- This allows a user to choose which functions or commands to execute based on **real-time analysis.**

- The `read -p "prompt" variable` command is used to **display a prompt** and **store user input** in a specified variable without moving to a new line.
	- ![[Pasted image 20250802110649.png]]

- A `case` statement can then be used to evaluate the variable and execute different blocks of code based on the user's input.

## Output

- For long-running scripts, it is often desirable to view the output in **real-time** while also saving it to a **file**.
  
  
- The `tee` utility accomplishes this by reading from standard input and writing to both standard output (the screen) and a specified file simultaneously.


- It is used in conjunction with a pipe (`|`). For example: `command | tee output.txt`.


- The `-a` (or `--append`) flag can be used with `tee` to append new data to the file instead of overwriting its contents.


## References:

https://academy.hackthebox.com/module/21/section/124