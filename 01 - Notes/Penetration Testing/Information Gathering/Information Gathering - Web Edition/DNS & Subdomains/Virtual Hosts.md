
2025-09-18 10:59

Tags: #web  

## Virtual Hosts

- **Virtual Hosting** is a method used by **web servers** (like Apache or Nginx) to **host multiple websites on a single server** with a single IP address.

- This is achieved by using the **HTTP `Host` header**. When a browser sends a request, it *includes the domain name it's trying to reach* in this header. The web server reads this header to determine which website's content to serve.

![Sequence diagram showing interactions between Browser, WebServer, VirtualHostConfig, and DocumentRoot. Includes HTTP request, server response, and file access steps.](https://mermaid.ink/svg/pako:eNqNUsFuwjAM_ZUop00CPqAHDhubuCBNBW2XXrzUtNFap3McOoT496WUVUA3aTkltp_f84sP2rgcdaI9fgYkgwsLBUOdkYqnARZrbAMk6oFd65HHiTd8XyPvfku9WpYA1dJ5eXS0tcW4ZOFMqJEkdU4y6vNnqul8PvRO1HKzeVFpp9KLumvbdmapAsItoy1KmRlX3_fwAXTd4OkLakuoOjVqiZAj_7_PaJJEPVvK1QrElJYK1UcDg1h3HmOEmV4LSlEC0-CA6i24Zb406IRhizuM7BV6BVFCit4FNuh77GX9DeGfmEu-s_mD4b5x5PH2Y4aqhfVNBftufomsGemJrpFrsHncqkOHy7SUWGOmk3jNgT8yndEx1kEQt96T0YlwwIlmF4pSJ1uofHyFJgf52cchirkVx6t-aU-7e_wG--_4bQ)


#### VHosts vs. Subdomains

- **Subdomains** are part of the **Domain Name System (DNS)**. They are extensions of a main domain (e.g., `blog.example.com`) and *have their own DNS records that point to an IP address.*

- **Virtual Hosts (VHosts)** are configurations on the **web server** itself. They define *how the server should respond to requests for different domains or subdomains* that resolve to its IP address.

- A VHost can exist *without a public DNS record* and can be discovered through a technique called **VHost fuzzing**, which involves **testing a list of potential hostnames against a target IP.**


## Types of Virtual Hosting

- **Name-Based:** The most common type. It uses the **`Host` header** to differentiate between sites. It's cost-effective as it doesn't require multiple IP addresses.

- **IP-Based:** Each website is assigned a *unique IP address*. The server determines which site to serve based on the destination IP of the request.

- **Port-Based:** Different websites on the same IP address are accessed via *different port* numbers (e.g., `:80`, `:8080`).

## Discovering Virtual Hosts

- Specialized tools can automate the process of finding VHosts. Key tools include **gobuster**, **Feroxbuster**, and **ffuf**.


- **Gobuster** can be used in `vhost` mode to brute-force potential hostnames. It sends HTTP requests to a target IP, **modifying the `Host` header** with names from a **wordlist** to see which ones return a valid response.

- A typical **`gobuster` command** for this is:
	- `gobuster vhost -u http://<target_IP> -w <wordlist_path> --append-domain`
		- `--append-domain` flag appends the base domain to each word in the wordlist. (required)
		- `-t` flag to increase the number of threads for faster scanning.
		- `-k` flag can ignore SSL/TLS certificate errors.
		- `-o` flag to save the output to a file for later analysis.
		- `--domain` used when you need to add domain name for the search (when using IP address in `-u`)
		- **Remember to set the IP address to hostname in /etc/hosts**


## References:

https://academy.hackthebox.com/module/144/section/1257