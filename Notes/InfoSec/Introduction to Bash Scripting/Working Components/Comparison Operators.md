
2025-07-31 10:22

Tags: #bash  

## Comparison Operators

- Comparison operators in Bash are used to compare values. They are categorized based on the type of data they operate on.
	- **String Operators**: Compare textual data.
	  
	- **Integer Operators**: Compare numerical data.
	  
	- **File Operators**: Test attributes of files and directories.
	  
	- **Logical Operators**: Combine or negate conditions.


## String Operators

- These operators are used for comparing strings. It is critical to **enclose string variables in double quotes** (e.g., `"$1"`) to *ensure they are treated as a single string*, preventing errors.
  
	- `==`: Checks if strings are **equal**.
		- Can use `*<string>*` to see if the 1st string **contains** the 2nd string
		  
	- `!=`: Checks if strings are **not equal**.
	  
	- `<`: Checks if a string is less than another in **ASCII alphabetical order**.
	  
	- `>`: Checks if a string is greater than another in **ASCII alphabetical order**.
	  
	- `=~`: Check if strings **contain** other string (regex only)
	  
	- `-z`: Checks if a string is **empty** (null).
	  
	- `-n`: Checks if a string is **not empty** (not null).


- **Note**: The `<` and `>` operators for string comparison must be used within **double square brackets** (`[[ ... ]]`).

## Integer Operators

- These operators are specifically for numerical comparisons.
	- `-eq`: is **equal to**
	  
	- `-ne`: is **not equal to**
	  
	- `-lt`: is **less than**
	  
	- `-le`: is **less than or equal to**
	  
	- `-gt`: is **greater than**
	  
	- `-ge`: is **greater than or equal to**


## File Operators

- These operators, also known as "file test operators," **check for the existence and properties of files or directories.**
  
	- `-e`: Checks if the file **exists**.
	  
	- `-f`: Checks if the path points to a regular **file**.
	  
	- `-d`: Checks if the path points to a **directory**.
	  
	- `-L`: Checks if the path is a **symbolic link**.
	  
	- `-s`: Checks if the file size is **greater than 0**.
	  
	- `-r`: Checks if the file has **read permission**.
	  
	- `-w`: Checks if the file has **write permission**.
	  
	- `-x`: Checks if the file has **execute permission**.
	  
	- `-O`: Checks if the **current user owns** the file.
	  
	- `-G`: Checks if the file's **group ID matches** the current user's.
	  
	- `-N`: Checks if the file was **modified since it was last read**.


## Logical Operators

- These operators are used to create complex conditional checks by combining or inverting the results of other comparison operations.
	- `!`: **NOT** (negates the result of the following expression).
	  
	- `&&`: **AND** (true only if both conditions are true).
	  
	- `||`: **OR** (true if at least one of the conditions is true).
## References:

