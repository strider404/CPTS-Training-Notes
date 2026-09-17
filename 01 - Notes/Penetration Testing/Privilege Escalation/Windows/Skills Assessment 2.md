
2026-05-28 18:08

Tags: #escalation 

## Skills Assessment 2

- Try LaZagne, SessionGopher,SharpChrome found nothing

- Try Winpeass
	- ![[Screenshot_20260528_182457.png]]
	- Found it: Inl@n3fr3ight_sup3rAdm1n!

- Exploits
	- ![[Pasted image 20260528183048.png]]
	-   CVE-2018-8544 KB4467708 [Critical] Remote Code Execution

	    CVE-2020-0796 KB4551762 [Critical] Remote Code Execution

	    CVE-2020-1472 KB4601345 [Critical] Elevation of Privilege

	    CVE-2021-1675 KB5003635 [Critical] Remote Code Execution

	    CVE-2021-22947 KB5009545 [Critical] Remote Code Execution

	    CVE-2021-24091 KB4601315 [Critical] Remote Code Execution
	
	    CVE-2021-34527 KB5004947 [Critical] Remote Code Execution

	    CVE-2025-47981 KB5062557 [Critical] Remote Code Execution

	    CVE-2025-59287 KB5070883 [Critical] Remote Code Execution

	    CVE-2018-0886 KB4556799 [Important] Remote Code Execution

	    CVE-2018-8411 KB4464330 [Important] Elevation of Privilege

	    CVE-2018-8423 KB4464330 [Important] Remote Code Execution

	    CVE-2018-8453 KB4464330 [Important] Elevation of Privilege

	    CVE-2018-8550 KB4467708 [Important] Elevation of Privilege

	    CVE-2018-8584 KB4467708 [Important] Elevation of Privilege

	    CVE-2019-0543 KB4480116 [Important] Elevation of Privilege

	    CVE-2019-0552 KB4480116 [Important] Elevation of Privilege

	    CVE-2019-0555 KB4487044 [Important] Elevation of Privilege

	    CVE-2019-0570 KB4480116 [Important] Elevation of Privilege

	    CVE-2019-0571 KB4480116 [Important] Elevation of Privilege


- whoami /priv
	- ![[Screenshot_20260528_191038.png]]


- No sus services
	- ![[Pasted image 20260528191224.png]]

- SharpUp
	- ![[Pasted image 20260528191702.png]]


- Tried PrintNightmare, HiveNightmare


- Locate Mozilla Maintenance Service
	- ![[Screenshot_20260528_192909.png]]


- Has the R+X permission
	- ![[Screenshot_20260528_193121.png]]


- Try CVE-2020-0668
	- See the [Kernel Exploit lecture](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FPenetration%20Testing%2FPrivilege%20Escalation%2FWindows%2FAttacking%20the%20OS%2FKernel%20Exploits)
	- ![[Screenshot_20260529_161031.png]]
	- Try windows/x64/shell_reverse_tcp payload
	- Get the shell
	- ![[Pasted image 20260529172104.png]]
	- Dump sam+system
	- ![[Pasted image 20260529172223.png]]
	- ![[Pasted image 20260529172243.png]]



## References:

https://academy.hackthebox.com/app/dashboard