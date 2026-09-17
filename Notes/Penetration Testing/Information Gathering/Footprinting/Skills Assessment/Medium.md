
2025-09-15 09:45

Tags: #footprint #hands-on 

## Medium

- First, **nmap**

- Found **port 2049**, NFS, [mount the shared folder](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FPenetration%20Testing%2FInformation%20Gathering%2FFootprinting%2FHost%20Based%20Enumeration%2FNFS) 

- Get the first credit (remember to use ls -la), **find everything you can, especially their home folder**

- Get the **ADMINISTRATOR** account (sa:87N1ns@slls83)

- Login to **SQL Management Studio** running with ADMINISTRATOR

- Edit the first 200 entries and find the flag


## References:

https://academy.hackthebox.com/module/112/section/1079