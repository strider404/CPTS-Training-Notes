
2025-08-19 11:52

Tags: #nmap  

## Security Components

- **Firewall**: A system that monitors network traffic and blocks or allows packets based on a set of security rules. It can **drop** packets (no response) or **reject** them (sends an error response).

- **IDS (Intrusion Detection System)**: A passive system that scans network traffic for malicious activity or policy violations and reports them.

- **IPS (Intrusion Prevention System)**: An active system that complements an IDS by automatically taking defensive actions, such as blocking the source IP address of a perceived attack.

## Nmap Evasion Techniques

- **TCP ACK Scan (`-sA`)**: This scan sends TCP packets with *only the ACK flag set*. Firewalls often pass these packets because they can't determine if the connection originated internally or externally, making this scan useful for mapping out firewall rulesets. An `unfiltered` response indicates the port is reachable (either open or closed), while a `filtered` response means a firewall is blocking the packet.
	- ![[Pasted image 20250819115406.png]]


- **Detecting IDS/IPS**: Detection is challenging. A common method is to perform scans from a disposable IP address (like a VPS). If the IP gets blocked, it confirms the presence of an active IPS, signaling the need for more covert methods.


- **Decoys (`-D RND:X`)**: This technique masks the true source of the scan by i*ncluding multiple spoofed (decoy) IP addresses* in the packet headers alongside the real one. The target's logs will show connection attempts from all the decoy IPs, making it difficult to identify the actual attacker.
	- ![[Pasted image 20250819115426.png]]


- **Source IP Spoofing (`-S`)**: Allows specifying a *different source IP address* for the scan. This can be used to test or bypass firewall rules that filter traffic based on source network ranges.
	- ![[Pasted image 20250819115517.png]]


- **Source Port Manipulation (`--source-port`)**: This method sends scan packets from a s*pecific source port*. Using a commonly trusted port, **such as DNS (port 53)**, can often bypass weak firewall rules that allow all traffic originating from that port, potentially revealing ports that were previously shown as `filtered`.
	- ![[Pasted image 20250819115600.png]]

## References:

https://academy.hackthebox.com/module/19/section/106