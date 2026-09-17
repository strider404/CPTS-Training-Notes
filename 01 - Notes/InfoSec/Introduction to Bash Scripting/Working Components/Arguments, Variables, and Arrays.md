
2025-07-31 09:56

Tags: #bash  

## Arguments & Script Execution

- **Positional Arguments**: Bash scripts can accept command-line arguments, which are automatically assigned to special variables called positional parameters.
	- `$0` is reserved for the **name of the script itself.**
	  
	- `$1`, `$2`, `$3`, ..., `$9` represent the first nine **arguments** passed to the script.

- More than 9: `"${@}"`

- **Execution**: To run a script directly (e.g., `./script.sh`), it must have **execute permissions**
	- **Permissions** are granted using the command: `chmod +x script_name.sh`.
	  
	- Alternatively, a script can be executed without execute permissions by passing it as an argument to its interpreter, for example: `bash script_name.sh`.


## Special Variables

- Bash utilizes several special variables that provide metadata about the script's execution environment. The Internal Field Separator (IFS) is used to parse these arguments.
	- `$#`: Contains the **total number of arguments** passed to the script (excluding `$0`).
	  
	- `$@`: An **array** construct containing **all command-line arguments** as individual strings.
	  
	- `$$`: The **Process ID (PID)** of the currently running script.
	  
	- `$?`: The **exit status** of the **most recently executed command**. A value of `0` indicates success, while a non-zero value (e.g., `1`) indicates failure.
	  
	- `${#<var>}`: To **count** the number of characters in that variable


## Variables

- **Declaration & Assignment**: Variables are assigned *without* a preceding dollar sign (`$`). There must be *no spaces* around the equals (`=`) sign.
	- **Correct**: `variable="value"`
	  
	- **Incorrect**: `variable = "value"`


- **Usage**: To *access the value* stored in a variable, it must be prefixed with a *dollar sign* (e.g., `echo $variable`).


- **Typing**: Bash does not enforce strict variable types in the same way as languages like C++ or Java.
	- By default, **all variables are treated as strings.**
	  
	- However, Bash can **perform arithmetic operations on variables containing only digits**. It is also possible to explicitly declare a variable as an integer using `declare -i variable_name`.

## Arrays

- **Definition**: Arrays are variables that can store an ordered sequence of multiple values.
  
- **Declaration**: Arrays are typically declared by enclosing a space-separated list of values in parentheses.
    
    - Example: `domains=(domain1.com domain2.com domain3.com)`


- **Accessing Elements**:
	- Individual elements are accessed using a zero-based index within square brackets: `${array[index]}`.
	  
	- **Example**: `echo ${domains[0]}` would output `domain1.com`.

- **Quoting**: Using double (`"`) or single (`'`) quotes around multiple items in an array declaration will cause them to be treated as a single element.
	- Example: `domains=("item1 item2" item3)` creates an array with two elements: `item1 item2` at index 0 and `item3` at index 1.

## References:
https://academy.hackthebox.com/module/21/section/125
