
2026-05-19 18:57

Tags:  #escalation 

## Linux Hardening

- **Updates and Patching**
    - Consistently patch kernels and third-party services to remove "low-hanging fruit" vulnerabilities.
        
    - Automate update processes using native packages like `unattended-upgrades` (Debian/Ubuntu) or `yum-cron` (Red Hat).


- **Configuration Management**
    - Audit all world-writable files, directories, and SUID binaries.
        
    - Enforce the use of absolute paths in cron jobs and sudo privileges.
        
    - Prevent cleartext credentials from being stored in world-readable files.
        
    - Regularly clean up user home directories and shell history files (e.g., `.bash_history`)
        
    - Restrict low-privileged users from modifying custom libraries called by other programs.
        
    - Uninstall unnecessary packages and services to minimize the attack surface.
        
    - Implement advanced access control mechanisms, such as SELinux.


- **User and Access Management**
    - Limit the total number of user and administrator accounts on the system.
        
    - Actively log and monitor all valid and invalid logon attempts.
        
    - Enforce strict password policies that favor long passphrases and prevent password reuse (utilizing `/etc/security/opasswd` and PAM modules).
        
    - Apply the principle of least privilege to user group assignments and sudo rights.
        
    - Utilize automation tools (Puppet, SaltStack, Zabbix, Nagios) to perform automated security checks, remote remediation, and binary checksum verification.


- **Auditing and Compliance**
    - Establish tailored security baselines using established frameworks (DISA STIGs, ISO27001, PCI-DSS, HIPAA) as reference guides, rather than definitive checklists.
        
    - Treat configuration audits as a supplement to—not a replacement for—hands-on vulnerability scanning and penetration testing.
        
    - **Tooling:** Use **Lynis**, a powerful Unix auditing tool, to scan configurations and uncover privilege escalation paths. Lynis provides a Hardening Index, detailed warnings, and remediation suggestions (running it as the `root` user yields the most comprehensive results).

## References:

