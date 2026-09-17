
2025-08-02 15:53

Tags: #bash  

## Flow Control - Branches

- **Flow Control Branches**: Include `if-else` and `case` statements.

- **Case Statements**:
	- Also known as `switch-case` in languages like C/C++, and C#.
	  
	- They compare an expression against specific, exact patterns or values.
	  
	- Unlike `if-else`, they cannot evaluate general boolean conditions like "greater-than".

- **Syntax**:
	- The structure begins with `case <expression> in` and ends with `esac`.
	  
	- Each condition is a `pattern)` followed by `statements`.
	  
	- Each block of statements must end with a double semicolon `;;`.
	  
	- **Example**:
	  `case <expression> in`
			`pattern_1 ) statements ;;`
			`pattern_2 ) statements ;;`
			`pattern_3 ) statements ;;`
		`esac`

![[Pasted image 20250802155621.png]]


## References:
https://academy.hackthebox.com/module/21/section/135
