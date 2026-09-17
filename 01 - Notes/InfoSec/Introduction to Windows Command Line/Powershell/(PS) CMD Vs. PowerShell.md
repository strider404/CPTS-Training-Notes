
2025-04-14 09:44

Tags: #windows #shell #hands-on  

## CMD Vs. PowerShell

| Feature                | CMD                                                                                                                                               | PowerShell                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Language**           | Batch & basic CMD commands                                                                                                                        | Supports CMD, Batch, PS cmdlets, aliases                                                                                             |
| **Command Piping**     | The output from one command ==cannot be passed== into another directly as a structured object, due to the limitation of handling the text output. | The output from one command ==can be passed== into another directly as a structured object resulting in more sophisticated commands. |
| **Output**             | Text-only                                                                                                                                         | Object-based                                                                                                                         |
| **Parallel Execution** | Sequential only                                                                                                                                   | Supports multithreading                                                                                                              |
| **Extensibility**      | Limited                                                                                                                                           | Fully scriptable; integrates with .NET & other too                                                                                   |

- More advanced functions than CMD, but logs are recorded more extensively
	- -> Need stealthy -> Use CMD

- Access Powershell
	- Windows Seach
	- Windows Terminal
	- Windows Powershell ISE (an IDE-like (not really) environment for Powershell)
	- CMD (command `powershell`)

- Most CMD commands work in Powershell

## Getting Help

- `Get-Help <cmdlet>` – Shows usage info.
	- can also be used to show all commands with patterns
		- `Get-Help *-Service`

- `Update-Help` – Downloads the latest help files.


- `Get-Help <cmdlet> -Online` – Opens official docs.


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1616)