
2025-04-16 10:58

Tags: #windows #shell #hands-on 

## Creating/Moving/Deleting Files & Directories

|Command|Alias|Description|
|---|---|---|
|`Get-Item`|`gi`|Retrieves an object (file, folder, etc.)|
|`Get-ChildItem`|`ls`, `dir`, `gci`|Lists folder contents|
|`New-Item`|`md`, `mkdir`, `ni`|Creates new files/folders|
|`Set-Item`|`si`|Modifies object properties|
|`Copy-Item`|`copy`, `cp`, `ci`|Duplicates an object|
|`Rename-Item`|`ren`, `rni`|Renames an object|
|`Remove-Item`|`rm`, `del`, `rmdir`|Deletes an object|
|`Get-Content`|`cat`, `type`|Displays file content|
|`Add-Content`|`ac`|Appends to a file|
|`Set-Content`|`sc`|Overwrites file content|
|`Clear-Content`|`clc`|Clears file content without deleting the file|
|`Compare-Object`|`diff`, `compare`|Compares objects and their content|

- Change many names: `get-childitem -Path *.txt | rename-item -NewName {$_.name -replace ".txt",".md"}`
	- -NewName's parameter is written in [ScriptBlock](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_script_blocks?view=powershell-7.5)

- `Get-ChildItem`:
	- `-recurse`: recursively (đệ quy), also displays its child directories' contents (display ALL)

- `Measure-Object`: Count the OUTPUT
## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1619)