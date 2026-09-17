
2025-04-21 11:47

Tags: #windows #shell #hands-on 

## Scripts vs Modules

- **Scripts** are ==single executable files== with cmdlets/functions. (can execute directly)

- **Modules** are ==collections of scripts and metadata==, offering reusable functionality. (needs to be imported)

- **File Extensions**:
	- `.ps1` – PowerShell **script** files
	- `.psm1` – PowerShell **module** files
	- `.psd1` – PowerShell **data** file detailing the contents of a PowerShell module in a table of **key/value** pairs

- Module Structure:
	- **Module Directory**: Stored in `$env:PSModulePath` for easy importing.
	- **Manifest File (`.psd1`)**: Describes the ==module, contents, author, dependencies==, etc.
	- **Code File (`.psm1` or `.ps1`)**: Contains the actual PowerShell logic.
	- **Supporting Resources**: Optional help files or dependencies.


## Building PowerShell Module

#### Making a Directory to Hold Our Module

- Should be within **$env:PSModulePath**

- Use `mkdir`

#### Module Manifest

- `.psd1` file

- **Functions**:
	- **Describes** the module’s contents and metadata (e.g., version, author, description).
	- **Defines prerequisites**, such as required PowerShell version, .NET CLR version, and dependent modules
	- **Controls processing**, including associated script, format, and type files.
	- **Manages exports**, specifying which functions, variables, aliases, and cmdlets the module makes available.

- `New-ModuleManifest`: create **new manifest** file
	- `-PassThru`: print what is in the file
	- e.g., `New-ModuleManifest -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psd1 -PassThru`

- Can edit file in text editors (Vim, VSCode)

- Create **Script (Code) file**: use `ni`

## Scripting in PowerShell

- Import Module: `Import-Module`

- Variables: `$` (`$HostName`)

- Function: `function <name> {}`

- **Get-Help** section: above the function with `<#.....#>` (when call `Get-Help`, it will be displayed)
	- Keywords: `.<keyword>`

- **Protecting** Functions: `Export-ModuleMember` (only specific functions and variables can be exported)
	- e.g., `Export-ModuleMember -Function Get-Recon -Variable $Hostname`

## Scope

| **Scope** | **Description**                                                                                                                                                                                                                                                   |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Global    | This is the default scope level for PowerShell. It affects all objects that exist when PowerShell starts, or a new session is opened. Any variables, aliases, functions, and anything you specify in your PowerShell profile will be created in the Global scope. |
| Local     | This is the current scope you are operating in. This could be any of the default scopes or child scopes that are made.                                                                                                                                            |
| Script    | This is a temporary scope that applies to any scripts being run. It only applies to the script and its contents. Other scripts and anything outside of it will not know it exists. To the script, Its scope is the local scope.                                   |

- Very long, should search for other sources 

- [about_Scopes - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-7.5&viewFallbackFrom=powershell-7.2)
## References:

