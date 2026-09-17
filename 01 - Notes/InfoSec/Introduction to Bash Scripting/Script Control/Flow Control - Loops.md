
2025-08-02 11:13

Tags: #bash  

## Flow Control - Loops

- **Purpose**: To control the execution flow of a script for efficiency and error-free processing.

- **Structures**: Control structures are categorized as either branches or loops.
	- **Branches**: `if-else` conditions, `case` statements.
	  
	- **Loops**: `for`, `while`, and `until` loops.

- **Mechanism**: Execution is generally governed by logical expressions that evaluate to a boolean value (`true` or `false`).

## for Loops

- **Function**: Executes a set of commands for each item in a specified list, array, or data source. The loop runs as long as it has items to process.

- **Common Use Cases**:
	- Iterating over values in an array.
	- Scanning a list of hosts or ports.
	- Automating enumeration tasks by executing commands for known services.

- **Syntax**: `for variable in [list]; do [commands]; done`
	- e.g., `for i in {1..40}`

## while Loops

- **Function**: Executes a block of code repeatedly as long as a given condition remains **true**.
  
- **Key Requirement**: A counter or another mechanism is necessary to eventually alter the condition to `false`, thereby preventing an infinite loop.

- **Syntax**: `while [ <condition> ]; do [commands]; done`

- **Control Commands**:
	- `break`: Terminates the loop's execution immediately.
	  
	- `continue`: Skips the remainder of the current iteration and proceeds to the next

## until Loops

- **Function**: Executes a block of code repeatedly as long as a given condition remains **false**. The loop terminates when the condition becomes `true`.
  
- **Comparison**: It functions as the logical opposite of a `while` loop.
  
- **Prevalence**: Described as being relatively rare compared to `while` loops.
## References:

