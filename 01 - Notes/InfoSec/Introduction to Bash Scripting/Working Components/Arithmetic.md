
2025-08-02 10:36

Tags: #bash   

## Arithmetic

- **Arithmetic Operators**: Bash supports seven primary arithmetic operators for mathematical calculations.
	- Addition: `+`
	  
	- Subtraction: `-`
	  
	- Multiplication: `*`
	  
	- Division: `/`
	  
	- Modulus (remainder): `%`
	  
	- Increment: `variable++` (increases value by 1)
	  
	- Decrement: `variable--` (decreases value by 1)



- **Syntax for Evaluation**: Arithmetic operations in Bash are typically performed within double parentheses.
	- To substitute the result of an expression into a command (e.g., `echo`), use the syntax `$((expression))`.
		- e.g., `echo "Addition: 10 + 10 = $((10 + 10))"`
		  
	- To simply perform the operation (e.g., modifying a variable), use `((expression))`.
		- e.g., `((stat--))`

- **Variable Length**: The length of a string variable can be determined using the syntax `${#variable}`, which **counts** the total number of characters.
	- Or `echo $variable | wc -c` to count **blanks**

## References:

https://academy.hackthebox.com/module/21/section/127