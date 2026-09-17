
2025-04-14 10:34

Tags: #windows #shell  
## Cmdlets

- **Cmdlets**: ==single-function commands== in PowerShell that follow a ==Verb-Noun== syntax (e.g., `Test-WSMan`)

- Unlike PowerShell functions, cmdlets are ==compiled==, typically in C#

## PowerShell Modules

- **Module**: a ==package== containing ==cmdlets, scripts, functions, and metadata==, designed for reuse and sharing.

- Contain:
	- `.psd1`: Manifest file with metadata (author, version, compatibility).
	- `.psm1`: Contains the actual PowerShell code.

## Managing Modules

- Import modules -> Can ==use that modules' cmdlets==

- `Get-Module`: Shows loaded modules.

- `Get-Module -ListAvailable`: Lists all installed modules.

- `Import-Module`: Loads a module into the current session (e.g., `Import-Module .\PowerSploit.psd1`)
	- Modules not in `PSModulePath` must be imported manually

- Modify `$env:PSModulePath` or place modules in default paths to make them persistently available -> easier to be recognized -> only load needed modules

## Execution Policy

- PowerShell's **execution policy** is not a security feature, but a ==control mechanism== for script execution behavior

- By default, the policy may ==prevent the running of scripts== (e.g., **Restricted**), causing import failures

- `Get-ExecutionPolicy` to view current policy

- `Set-ExecutionPolicy` to change policy
	- Setting it to `Undefined` or `Bypass` removes restrictions.
	- `-scope Process`: applied only in this session
	- e.g., `Set-ExecutionPolicy undefined -scope Process`

## Using Modules

- To view available commands in a module: `Get-Command -Module <modulename>`

- [PowerShell Gallery](https://www.powershellgallery.com/): Central ==repository== for PowerShell modules/scripts

- **PowerShellGet**: a ==built-in module== help us ==interact with the PowerShell Gallery==
	- Use `Get-Command -Module PowerShellGet` to view commands

- Simultaneously find + install module form Powershell Gallery:
	- `Find-Module -Name AdminToolbox | Install-Module`

- Modern PowerShell auto-imports Gallery modules ==upon first use==, but other sources (Github) must imported in each session


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1636)