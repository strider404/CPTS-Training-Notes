
2025-04-12 12:27

Tags: #windows #shell #hands-on

## Environment Variables

- Environment variables are **key-value pairs** used to configure system and application behavior
	- Not case-sensitive
	- Can include **spaces and numbers**, but **not start with a number** or contain an equal sign (=)
	- Referred to using the `%VARIABLE_NAME%` syntax (e.g., `%WINDIR%`).

## Variable Scope

- Scope determines where a variable is accessible:
	- **Global Scope**: Variables accessible **system-wide**. Example: `%WINDIR%` is visible to all users
	- **Local Scope**: Variables defined within **a single session or user context.** Example: A variable set by Alice isn’t visible to Bob.

## Windows Scope Categories

| Scope       | Description                                                                  | Access Required              | Registry Location                                                                 |
| ----------- | ---------------------------------------------------------------------------- | ---------------------------- | --------------------------------------------------------------------------------- |
| **System**  | Global variables defined by the OS, available to ==all users==.              | Local/Domain Admin           | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment` |
| **User**    | Variables defined by a ==specific user==, accessible only to them.           | Current user or Admin        | `HKEY_CURRENT_USER\Environment`                                                   |
| **Process** | ==Temporary variables== specific to the current process, not stored on disk. | Process/user that defined it | Stored in memory (not the registry)                                               |

## Managing Environment Variables

- **`set`**: Lists all environment variables if run alone
	- `set <%VARIABLE_NAME%>`: display that specific variable (set PATH)
	- `set <%VARIABLE_NAME%>= <Value>`: change or create a variable equal to the value (**Only in this session**)
		- Can use `set <%VARIABLE_NAME%>=` to delete in this session

- **`echo`**: Used to print the value of a specific environment variable. E.g.,: `echo %VAR%`

- `setx <%VARIABLE_NAME%> <Value>`: change or create a variable equal to the value (**Permanent**)
	- e.g., `setx DCIP 172.16.5.2`
	- Deleting: `setx DCIP ""`


## Important Environment Variables

| Variable Name         | Description                                                                                                                                                                                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `%PATH%`              | Specifies a set of ==directories(locations)== where executable programs are located.                                                                                                                                                                                                          |
| `%OS%`                | The ==current operating system== on the user's workstation.                                                                                                                                                                                                                                   |
| `%SYSTEMROOT%`        | Expands to `C:\Windows`. A system-defined read-only variable containing the ==Windows system folder==. Anything Windows considers important to its core functionality is found here, including important data, core system binaries, and configuration files.                                 |
| `%LOGONSERVER%`       | Provides us with the ==login server== for the currently active user followed by the machine's hostname. We can use this information to know if a machine is joined to a domain or workgroup.                                                                                                  |
| `%USERPROFILE%`       | Provides us with the location of the ==currently active user's home directory==. Expands to `C:\Users\{username}`.                                                                                                                                                                            |
| `%ProgramFiles%`      | Equivalent of `C:\Program Files`. This location is where ==all the programs are installed on an `x64` based system==.                                                                                                                                                                         |
| `%ProgramFiles(x86)%` | Equivalent of `C:\Program Files (x86)`. This location is where ==all 32-bit programs== running under `WOW64` are installed. Note that this variable is only accessible on a 64-bit host. It can be used to indicate what kind of host we are interacting with. (`x86` vs. `x64` architecture) |
- FULL: [Windows Environment Variables - Windows CMD - SS64.com](https://ss64.com/nt/syntax-variables.html)

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1611)