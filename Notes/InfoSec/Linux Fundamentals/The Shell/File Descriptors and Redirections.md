
2025-02-21 11:05

Tags: #linux #bash #hands-on

## File Descriptors


- File descriptor (`FD`): allow system to manage I/O operations
	- Think of it like a ticket (FD) you show the seller (OS) for lunch (resources). The action is I/O operations

- Default descriptors:
	- **Input: STDIN** - 0 (what you give to the command)
	- **Output: STDOUT** - 1 (valid results)
	- **Error: STDERR** - 2 (invalid results)


## Redirections

 ### **Redirect STDIN**

- Can use the =='<'== to redirect STDIN (EX: cat < file.txt)

- '<< EOF' to create a stream of STDIN (End-of-File)
![[Pasted image 20250221112136.png]]

 ### **Redirect STDOUT**
 
- =='>'== to redirect to a file, if already exists it will be overwritten

- =='>>'== to append existing file

 ### **Redirect STDERR**

- Same commands as STDOUT, should redirect to '==null device (/dev/null)==' to discard all error data
	- Ex: `2>/dev/null` '2' for **STDERR**

- Can be used to filter error results, combining with redirecting STDOUT (`2>/dev/null > results.txt`). Because there is no more errors after the `2>/dev/null` so no need to add 1 to the next option

### **Pipe**

- ==Output from this command become input for the next command==
	- `find /etc/ -name *.conf 2>/dev/null | grep systemd`



## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/79)