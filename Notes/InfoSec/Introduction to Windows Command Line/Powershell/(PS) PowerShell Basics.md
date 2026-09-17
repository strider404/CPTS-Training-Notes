
2025-04-14 10:01

Tags: #windows #shell #hands-on

## Navigation

- **`Get-Location`**: Shows the current working directory.

- **`Get-ChildItem`**: Lists contents of a directory (similar to `ls` or `dir`).

- **`Set-Location`**: Changes the current directory (`cd` equivalent).

## View File Content

- **`Get-Content`**: Displays the content of files (e.g., `.txt`, `.md`).

## Discovering Commands

- **`Get-Command`**: Lists all available cmdlets, aliases, and functions.
	- Filtered by:
		- `-verb` (e.g., `Get-Command -verb get`)
		- `-noun` (e.g., `Get-Command -noun windows*`)

## History

- **`Get-History`**: Shows commands from the current session.

- **`PSReadLine` module**:
	- ==Stores history across sessions in a file==
	- Sensitive keywords like "password" ,"asplaintext", "token", "apikey", "secret" are excluded from logs.
	- History file path: `C:\Users\<Username>\APPDATA\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`

## Clear Screen

- **`Clear-Host` / `clear` / `cls`**: Clears the terminal display.

## Hot Keys

|Shortcut|Function|
|---|---|
|`Ctrl + R`|Search through command history|
|`Ctrl + L`|Clear screen quickly|
|`Escape`|Clear current input line|
|`↑ / ↓`|Navigate command history|
|`F7`|Interactive TUI history viewer|
|`Ctrl + Alt + Shift + ?`|List all keyboard shortcuts|

## Tab Completion

-  **Tab / Shift + Tab**: Autocomplete commands or cycle options.

## Aliases

- **Alias** is ==another name== for a cmdlet, command, or executable file

- **`Get-Alias`**: Lists all available aliases.

- Common Aliases:
	- `ls` / `dir` / `gci` → `Get-ChildItem`
	- `cd` / `sl` / `chdir` → `Set-Location`
	- `cat` / `gc` / `type` → `Get-Content`
	- `pwd` → `Get-Location`
	- `curl` / `wget` → `Invoke-WebRequest`
	- `man` → `help`
	- `fl` → `Format-List`, `ft` → `Format-Table`

- **`Set-Alias`**: Create custom aliases (e.g., `Set-Alias gh Get-Help`).

## References:

