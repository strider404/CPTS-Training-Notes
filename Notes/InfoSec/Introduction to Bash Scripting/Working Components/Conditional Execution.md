
2025-07-30 15:32

Tags: #bash  

## Conditional Execution

- **Conditional execution** is a fundamental programming concept that allows a script to execute different sections of code *based on whether specific conditions are met*.

## Core Structure

- `if [ <condition> ]`: Starts the conditional block and checks if a `<condition>` is true.
	- Notice the **spaces** between `[]` and the condition
	  
- `then`: **Executes** the following code block if the `if` condition is true.

- `elif [ <condition> ]`: (short for "else if") Provides an alternative condition to check if the previous `if` or `elif` was false. You can use multiple `elif` statements.

- `else`: Provides a default code block to execute if all preceding `if` and `elif` conditions are false.

- `fi`: Marks the **end** of the entire conditional block.

#### Nested Condition

- Need to put `;then` after the parent condition
	- **Example**:
		- `if [ <condition_1> ];then`
			- `if [ <condition_2> ]`

#### Other components

- **Shebang (`#!`)**: The very first line of a script, like `#!/bin/bash`, which specifies the path to the interpreter that will execute the script.

- **Special Variables**: Shell variables with pre-defined meanings used for scripting logic.
	- `$#`: The **total number of arguments** passed to the script.
	  
	- `$0`: The **name of the script file** itself.
	  
	- `$1`: The **first argument** passed to the script.

- **Comparison Operators**: Used within the square brackets `[ ]` to compare values. The example uses `-eq` to test if two numbers are equal.
  
- **`exit` Command**: *Terminates* the script immediately. An argument like `exit 1` is commonly used to signal that an error occurred.


## References:

https://academy.hackthebox.com/module/21/section/132