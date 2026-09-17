
2025-03-08 08:00

Tags: #linux 

## Linux Security

- Update system: `apt update && apt dist-upgrade`

- Use firewall, SSH, use sudo instead of root rights, use the least privilege principle

- Use kernel-level mordule like SELinux

## TCP Wrappers

- TCP wrapper: allow which service can access the system based on restricting IP addresses or hostnames

- Only manage service-level access -> can't replace the firewall (work at network-level, can filter traffic before they reach the services, filter by ports and invidual packets too)

- Configure in /etc/hosts.allow and /etc/hosts.deny, in the link below


## References:

[Linux Fundamentals](https://academy.hackthebox.com/module/18/section/98)