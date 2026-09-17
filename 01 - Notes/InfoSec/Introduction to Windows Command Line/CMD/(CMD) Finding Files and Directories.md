
2025-04-11 10:42

Tags: #windows #shell #hands-on 

## Searching

- `where`: return the **directory** of a file
	- e.g., `where calc.exe`: returns `C:\Windows\System32\calc.exe`
	- `/R` to **recursively search** a specified directory:  `where /R C:\Users\student\ bio.txt`

- **Wildcard**: search for file types: `where /R C:\Users\student\ *.csv`

- `find`: Searches for **text strings** within files
	- `/V` – returns lines **not** containing the string.
	- `/I` – **case-insensitive** search.
	- `/N` – shows **line numbers**.
	- e.g., `find /N /I /V "IP Address" example.txt`  

 - `findstr`: same like `find` but closer to `grep`

- `comp`: Compares files **byte-by-byte**.
	- `/A` – ASCII output
	- `/L` – Line numbers
	- e.g., `comp .\file-1.md .\file-2.md`

- `fc`: Compares files **line-by-line**, more detailed than `comp`

- `sort.exe`: Alphabetically sorts file content
	- `/O <file>` – outputs result to another file.
	- `/unique` – **removes duplicates** from the result.
	- e.g.,  `sort.exe .\sort-1.md /unique`



## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1614)