
2025-08-21 11:48

Tags: #nmap #hands-on 

## Lab 3 - Hard

- Utilize options like `--source-port 53` really helpful to bypass some firewall

- Always use `-v` because sometimes nmap can't even finish

- You can also use `-Pn` or `-n` or `--disable-arp-ping` but they are not really necessary

- Use `nc` to connect to the port
	- Command like `ss -tulpn` helps to find the PID and kill it


## References:

https://academy.hackthebox.com/module/19/section/119