
2026-05-21 17:16

Tags: #escalation 

## Hyper-V Administrators

- **Core Privilege:** Grants full access to all Hyper-V features on the host system.


- **Virtualization Equals Domain Compromise:** If Domain Controllers (DCs) are **virtualized**, *Hyper-V admins are effectively Domain Admins.* They can clone the live DC, mount the virtual disk offline, and extract the `NTDS.dit` file to dump all domain NTLM hashes.

## File Permission Abuse (Hard Link Attack)

- **The Vulnerable Mechanism:** When a virtual machine is deleted, `vmms.exe` restores the original file permissions on the associated `.vhdx` file. Crucially, it performs this action as `NT AUTHORITY\SYSTEM` without impersonating the user.


- **The Exploit Path:** An attacker deletes the `.vhdx` file and creates a native hard link pointing to a protected SYSTEM file. When `vmms.exe` processes it, it inadvertently grants the attacker full control over the target SYSTEM file.


- **Prerequisites:** This relies on unpatched OS vulnerabilities (CVE-2018-0952 or CVE-2019-0841) or targeting third-party services that run as SYSTEM but can be started by unprivileged users.

## Exploitation Example (Mozilla Maintenance Service)

- **Target Selection:** Firefox installs the Mozilla Maintenance Service, which runs as SYSTEM and is a viable target.


- **Execution Steps:**
    1. Use the hard link proof-of-concept to force permissions changes on `C:\Program Files (x86)\Mozilla Maintenance Service\maintenanceservice.exe`.
        
    2. Take ownership of the file using the command: `takeown /F "C:\Program Files (x86)\Mozilla Maintenance Service\maintenanceservice.exe"`.
        
    3. Replace the legitimate executable with a malicious payload.
        
    4. Trigger the payload to gain a SYSTEM shell by starting the service: `sc.exe start MozillaMaintenance`.


- **Mitigation Status:** This specific hard link vector was patched by Microsoft in the March 2020 security updates.
## References:

