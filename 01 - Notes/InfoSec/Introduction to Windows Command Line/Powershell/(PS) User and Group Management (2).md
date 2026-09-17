
2025-04-15 14:46

Tags: #windows #shell #hands-on

## Adding/Removing/Editing User Accounts & Groups

- **User**:
	- `Get-LocalUser`: display the users on our host
	- `New-LocalUser`: Creating A New User (e.g.,`New-LocalUser -Name "JLawrence" -NoPassword`)
	- `Set-LocalUser`: Modifying a User (e.g., `Set-LocalUser -Name "JLawrence" -Password $Password -Description "CEO EagleFang"`)

- **Group**:
	- `Get-LocalGroup`: display the groups on our host
	- `Add-LocalGroupMember`: Adding a Member To a Group (e.g., `Add-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrence"`)
	- `Get-LocalGroupMember`: check users in specific group (e.g., `Get-LocalGroupMember -Name "Remote Desktop Users"`)

## Managing Domain Users and Groups

- Installing RSAT: The **Remote Server Administration Tools** (RSAT) must be installed to access the official `ActiveDirectory` PowerShell module
	- `Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online`

- `Get-ADUser`: to grab users in Active Directory (Domain user)
	- `-Filter *` : List all
	- `-Identity <name>`: List specific user
	- `-Filter {EmailAddress -like '*greenhorn.corp'}`: filter by attribute (EmaiAddress, GivenName, Surname,...)

- `Get-ADDomainController`: get the Domain Controller

- `New-ADUser`: create new AD user (Domain user)
	- e.g., `New-ADUser -Name "MTanaka" -Surname "Tanaka" -GivenName "Mori" -Office "Security" -OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"} -Accountpassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true`

- `Set-ADUser`: modify AD users (Domain user)
	- e.g., `Set-ADUser -Identity MTanaka -Description "Sensei to Security Analyst's Rocky, Colt, and Tum-Tum"`

## Adding Computer to AD Domain

- `Add-Computer`: Add a Local Computer to AD Domain
	- e.g., `Add-Computer -ComputerName ACADEMY-IAD-W10 -LocalCredential ACADEMY-IAD-W10\image -DomainName INLANEFREIGHT.LOCAL -Credential INLANEFREIGHT\htb-student_adm -Restart`

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1618)