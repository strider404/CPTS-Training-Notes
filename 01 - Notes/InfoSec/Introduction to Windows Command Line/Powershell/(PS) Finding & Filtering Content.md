
2025-04-17 09:51

Tags: #windows #shell  #hands-on

## PowerShell Output (Objects Explained)

- Powershell treats all **OUTPUT** as ==Object==

- **Object**: an individual instance of a ==class==
	- **Class**: like OOP, defining the structure of an object
		- **Properties**: its attributes, the data associates with the object
		- **Method**: its functions


## Finding and Filtering Objects

- `Get-Member`: ==get== an Object's Properties & Methods
	- e.g.,  `get-localuser Admin | get-member`

- `Select-Object`: ==see specific== Methods or Properties
	- Can specific which Properties or Methods
	- e.g., `Get-LocalUser administrator | Select-Object -Property *`
	- e.g., `Get-LocalUser * | Select-Object -Property Name,PasswordLastSet`

- `Sort-Object`: ==organize== data based on specific Properties & Methods
	- e.g.,`Get-Service | Select-Object -Property DisplayName,Name,Status | Sort-Object DisplayName | Format-List`

- `Where-Object`: filter based on ==Properties==
	- e.g., `Get-Service | Where-Object DisplayName -like '*Defender*'`

- `Select-String` (alias `sls`): Works like **grep** or **findstr**. Searches for ==regex/string== patterns in files
	- e.g., `Select-String "password", "credential", "key", "username"`


## Comparison Operators

- `-like`: Pattern matching with ==wildcards== (`'*Defender*'`)

- `-contains`: Exact match within a ==collection== (if an array contains a value)

- `-eq`: ==Exact value== match, case sensitive (compare 2 values)

- `-match`: ==Regex== match

- `-not`: ==Negates== a condition or checks for null

- More: [about_Comparison_Operators - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.5&viewFallbackFrom=powershell-7.2)


## Pipelines

- **Pipelines** (|): ==Chains== commands together, passing the output of one as input to the next (left to right execution).

- **`&&`**: Runs the next command only if ==the previous one succeeds.==

- **`||`**: Runs the next command only if ==the previous one fails.==

## Helpful Locations for Enumeration

- `C:\Users\<User>\AppData\` — App configs, temp files.

- `C:\Users\<User>\` — Home dir (hidden files like keys).

- PowerShell history:
    - `ConsoleHost_history.txt`
    - `(Get-PSReadlineOption).HistorySavePath`

- Clipboard contents: `Get-Clipboard`

- Scheduled tasks

## References: 
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1621)
