
2026-05-19 18:04

Tags: #linux  

## Sudo

- **Check sudo version**
	- `sudo -V | head -n1`

|**Vulnerability**|**CVE Identifier**|**Affected Versions**|**Core Exploit Mechanism**|
|---|---|---|---|
|**Heap-Based Buffer Overflow**|CVE-2021-3156|1.8.31, 1.8.27, 1.9.2, etc.|Compiling and executing a C-based exploit payload targeted at specific OS versions.|
|**Sudo Policy Bypass**|CVE-2019-14287|All versions < 1.8.28|Passing a negative User ID (`-1`) to trick `sudo` into executing a permitted command as root (ID `0`).|
## Heap-Based Buffer Overflow (CVE-2021-3156)

- **The Flaw:** This vulnerability sat undetected in `sudo` for over a decade. It involves a heap-based buffer overflow that occurs when parsing command-line arguments.


- **Identification:** An attacker can check their `sudo` version (`sudo -V`) and cross-reference it with their operating system release (`cat /etc/lsb-release`).


- **Exploitation:** By downloading and compiling a public Proof-of-Concept (PoC) like `sudo-hax-me-a-sandwich`, an attacker can target their specific OS build. Running the compiled exploit triggers the overflow and instantly drops the user into a root shell (`uid=0`).
	- ![[Screenshot_20260519_180712.png]]


## Sudo Policy Bypass (CVE-2019-14287)

- **The Flaw:** This exploit takes advantage of how `sudo` processes specific User IDs. It requires only one prerequisite: the attacker's user must be explicitly allowed to run _some_ command via `/etc/sudoers` (e.g., `ALL=(ALL) /usr/bin/id`).


- **Exploitation:** `sudo` allows users to execute commands by specifying a target User ID using the `-u#` flag. Root always has an ID of `0`. Due to a parsing error in older versions of `sudo`, passing a negative ID like `-1` (or its unsigned equivalent) wraps around and is interpreted as `0`.


- **Execution:** By running a command like `sudo -u#-1 id`, the system bypasses intended restrictions and runs the command directly as root.


## References:

