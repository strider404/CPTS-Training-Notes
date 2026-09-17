
2025-07-18 11:34

Tags: #ad #hands-on 

## Guided Lab Part I

- On **Server Manager** App, navigate to the right corner, choose Tools -> AD **Users** and Computers to manage them

- Use **Search** 

- To change the **GPOs**, navigate to the right corner, choose Tools -> Group Policy Manager

- **Duplicate** Policy (PS):
	- Copy it: `Copy-GPO -SourceName "Logon Banner" -TargetName "Security Analysts Control"`
	- Link it to desired OU: `New-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes`

- Right click to the GPO and click Edit to edit it


## References:
https://academy.hackthebox.com/module/74/section/708
