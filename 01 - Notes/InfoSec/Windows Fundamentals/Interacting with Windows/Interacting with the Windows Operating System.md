
2025-03-22 09:38

Tags: #windows  

- Explain ways to interact with the OS

## Graphical User Interface

- Allows point and click interactions -> suitable for both casual users and IT specialists

## Remote Desktop Protocol (RDP)

- Enables users to control the GUI over the network

- Using port 3382

- Often used by server admin through a VPN


## Windows Command Line 

- Command-line interface:
	- Command Prompt (CMD)
	- Powershell


## CMD

- Access by typing cmd in the Start or C:\Windows\system32\cmd.exe

## Powershell

- Designed toward system administrators

- Built in .NET framework, give user direct access to the file system


## Cmdlets

- Powershell uses cmdlets as its main commands

- Written in Verb-Noun structure (e.g.Get-ChildItem)

- Over 100 cmdlets

- Can use arguments (e.g. -Recurse)

## Aliases

- Shortcuts for cmdlets (e.g. cd for Set-Location and ls for Get-ChildItem)

- Need help: Get-Help

- get-alias to get aliases
	- returns the Alias, Name, Definition objects

## Running Scripts

- PowerShell ISE (Integrated Scripting Environment) allows users to write, run, debug scripts

- Scripts can be imported into the session (e.g., via Import-Module) to access their functions easily.

## Execution Policy

- Execution Policy used to prevent users from running malicious scripts

| **Policy**     | **Description**                                                                                                                                                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `AllSigned`    | ==All scripts can run==, but a trusted publisher must sign scripts and configuration files. This includes both remote and local scripts. We receive a prompt before running scripts signed by publishers that we have not yet listed as either trusted or untrusted. |
| `Bypass`       | ==No scripts or configuration files are blocked==, and the user receives no warnings or prompts.                                                                                                                                                                     |
| `Default`      | This sets the ==default execution policy==, `Restricted` for Windows desktop machines and `RemoteSigned` for Windows servers.                                                                                                                                        |
| `RemoteSigned` | ==Scripts can run but requires a digital signature== on scripts that are downloaded from the internet. Digital signatures are not required for scripts that are written locally.                                                                                     |
| `Restricted`   | This ==allows individual commands but does not allow scripts== to be run. All script file types, including configuration files (`.ps1xml`), module script files (`.psm1`), and PowerShell profiles (`.ps1`) are blocked.                                             |
| `Undefined`    | No ==execution policy is set for the current scope==. If the execution policy for ALL scopes is set to undefined, then the default execution policy of `Restricted` will be used.                                                                                    |
| `Unrestricted` | This is the ==default execution policy for non-Windows computers==, and it cannot be changed. This policy allows for unsigned scripts to be run but warns the user before running scripts that are not from the local intranet zone.                                 |

- Get policies: `Get-ExecutionPolicy -List`

- Change policies: `Set-ExecutionPolicy Bypass -Scope Process`



## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/460)