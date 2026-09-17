
2025-09-18 10:13

Tags: #web  

## Subdomain Bruteforcing

- **Definition**: An active technique for discovering subdomains by systematically testing a list of potential names against a target domain.

- **Goal**: To identify valid subdomains that may not be publicly linked.

- **Tools**:
	- `dnsenum`
	- `fierce`
	- `dnsrecon`
	- `amass`
	- `assetfinder`
	- `puredns`


## Process

- **Wordlist Selection**: Choose a list of potential subdomain names. This can be a general list, one targeted to a specific industry, or a custom-created one.

- **Iteration and Querying**: A tool automatically appends each name from the wordlist to the target domain (e.g., `admin` + `.example.com`).

- **DNS Lookup**: For each created name (e.g., `admin.example.com`), a DNS query is sent to see if it resolves to an IP address.

- **Filtering and Validation**: If a subdomain resolves, it is marked as valid. Further checks can be done to confirm it is active.

## `dnsenum`

- **Description**: A comprehensive Perl-based command-line tool for DNS reconnaissance.

- **Key Features**:
	- Enumerates various DNS records (`A`, `NS`, `MX`, etc.).
	  
	- Attempts DNS zone transfers.
	  
	- Performs subdomain bruteforcing using wordlists.
	  
	- Scrapes Google for additional subdomains.
	  
	- Conducts reverse DNS lookups and WHOIS queries.

- **Example Usage**: The text demonstrates using `dnsenum` with the `SecLists` wordlist to recursively find subdomains for `inlanefreight.com`.
	- `dnsenum --enum inlanefreight.com -f /path/to/wordlist.txt -r`
## References:

https://academy.hackthebox.com/module/144/section/**1253