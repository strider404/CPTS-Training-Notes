
2025-04-03 10:29

Tags: #windows #shell #hands-on 

## Files

## List Files & View Their Contents

- `more` displays file contents page by page.
	- `/S` to partly get rid of the space bar between lines

- `openfiles` (requires admin privileges) lists open files on a local or remote machine)

- `type` prints file contents and can concatenate multiple files
	- can redirect the output
	- e.g., can use `type <source> >> <destination>` to append 1 file to another


## Create And Modify A File

- `echo <text> > <file>`can create and append text to files

- `fsutil file createNew <filename> <size>` creates a file of a specified size

- `ren` (or `rename`) changes file names

## Input / Output

- **Output To A File**: 
	- The `>` operator writes command output to a file, overwriting existing content
		- e.g., `ipconfig /all > details.txt` saves the output to `details.txt`
	- The `>>` operator appends output to an existing file

- **Pass in a Text File to a Command**:
	- `<`: allows using file content as input for a command
		- e.g., `find /i "see" < test.txt` searches for "see" in `test.txt`

- **Pipe Output Between Commands**:
	- `|`: sends the output of one command directly to another.

- **Chaining Commands:
	- `&`: Runs multiple commands sequentially, ==regardless of success==.
	- `&&`: Runs the second command only if ==the first succeed==s.
	- `||`: Runs the second command only if ==the first fails==.


## Deleting Files

- `del` and `erase` can remove files, accepting directories, filenames, lists, or attributes.
	- can delete multiple files at once
	- e.g., `erase file1 file2`
	- `/A: <attribute>`: delete files with that attribute (R for read-only, H for hidden) 
	- e.g., `del /A:R *` delete all read-only files
	- `/F`: to force delete
	- If parsed a directory, only delete its content, not the directory itself

## Copying and Moving Files

- `copy` duplicates a file
	- To rename it, use the new name in the new directory
	- e.g., `copy secrets.txt C:\Users\student\Downloads\not-secrets.txt` (renamed to not-secrets.txt)
	- `/V`:  turn on file validation

- `move` relocates or renames files
	- e.g., `move bio.txt C:\Users\student\Downloads`

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1610)