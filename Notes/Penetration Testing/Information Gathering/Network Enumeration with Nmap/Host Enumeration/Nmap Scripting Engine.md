v
2025-08-19 10:32

Tags: #nmap  

## Nmap Scripting Engine

- **Nmap Scripting Engine (NSE)** is a feature within Nmap that allows users to *write and use scripts*, written in the *Lua* programming language, to automate a wide range of networking tasks.

#### NSE Script Categories

| **Category** | **Description**                                                                                                                             |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `auth`       | Determination of **authentication** credentials.                                                                                            |
| `broadcast`  | Scripts, which are used for host discovery by **broadcasting** and the discovered hosts, can be automatically added to the remaining scans. |
| `brute`      | Executes scripts that try to log in to the respective service by **brute-forcing** with credentials.                                        |
| `default`    | **Default** scripts executed by using the `-sC` option.                                                                                     |
| `discovery`  | Evaluation of **accessible** services.                                                                                                      |
| `dos`        | These scripts are used to check services for **denial of service** vulnerabilities and are used less as it harms the services.              |
| `exploit`    | This category of scripts tries to **exploit known vulnerabilities** for the scanned port.                                                   |
| `external`   | Scripts that use **external services** for further processing.                                                                              |
| `fuzzer`     | This uses scripts to **identify vulnerabilities** and unexpected packet handling by sending different fields, which can take much time.     |
| `intrusive`  | **Intrusive** scripts that could **negatively** affect the target system.                                                                   |
| `malware`    | Checks if some **malware** infects the target system.                                                                                       |
| `safe`       | Defensive scripts that do **not** perform **intrusive** and destructive access.                                                             |
| `version`    | Extension for **service** detection.                                                                                                        |
| `vuln`       | Identification of **specific vulnerabilities**.                                                                                             |

#### Execution

- **Default Scripts:** Use the `-sC` option to run all scripts in the `default` category.
    - `sudo nmap <target> -sC`


- **Specific Category:** Use the `--script <category>` flag to run all scripts from a specified category (e.g., `vuln`).
    - `sudo nmap <target> --script vuln`


- **Specific Scripts:** Define one or more specific script names using the `--script` flag, separated by commas.
    - `sudo nmap <target> --script banner,smtp-commands`


- **Aggressive Scans (`-A`)**
	- The aggressive scan option (`-A`) is a convenient shortcut that enables *multiple advanced scanning features* simultaneously.
	  
	- **It combines**:
	    - OS detection (`-O`)
	    - Service version detection (`-sV`)
	    - Traceroute (`--traceroute`)
	    - Default script scanning (`-sC`)


- **Example**: 
![[Pasted image 20250819104059.png]]

- It ran the `vuln` script and the known vulnerabilities of that port were displayed

## References:

https://academy.hackthebox.com/module/19/section/108