
2025-08-02 15:57

Tags: #bash  

## Functions

- There are two common **syntaxes** for defining a function in Bash:
    
    1. Using the `function` keyword: `function function_name { <commands> }`
       
    2. Using parentheses: `function_name() { <commands> }`

#### Parameter Passing

- Arguments can be passed to a function when it is called, similar to how arguments are passed to a script.
  
- Inside the function, these parameters are accessed using **positional parameters**: `$1` for the first argument, `$2` for the second, and so on.
  
- Each function has its own isolated set of positional parameters, which **do not conflict** with those of the main script or other functions.

![[Pasted image 20250802160111.png]]


#### Variable Scope

- By default, variables defined inside a shell function are **global**. This means they are accessible and can be modified anywhere in the script after their initial definition, even outside the function.
  
- To create a variable that is only accessible within the function (**local scope**), it must be explicitly declared with the `local` keyword.

#### Return Values

- Functions can communicate their **execution status** back to the calling process through a **return code** (an integer between 0 and 255).
    
    - A return code of `0` typically signifies **success**.
      
    - A **non-zero** code indicates an **error**.
      
    - The `return` command is used to explicitly set this code (e.g., `return 1`).
      
    - The **return code of the most recently executed function (or command)** is stored in the special variable `$?`.
        - **Have to use this** instead of just the function like in C++

![[Pasted image 20250802160513.png]]



- To "return" actual data (like a **string** or a **number**) from a function, two common methods are used:
	1. **Standard Output**: The function uses `echo` to print the result. The calling code can then capture this output using command substitution: `result=$(function_name)`.
	   
	2. **Global Variables**: The function assigns its result to a global variable, which can then be accessed by the main part of the script.

![[Pasted image 20250802160742.png]]


## References:

https://academy.hackthebox.com/module/21/section/130