
2025-03-08 22:06

Tags: #linux 

## Solaris

- Solaris is a Unix-based operating system often deployed in banking, finance and government because of its robustness, scalability, and enterprise-grade performance

- Solaris incorporates enhanced security mechanisms, including Role-Based Access Control (RBAC) and mandatory access controls.

- Is NOT open-source like Linux

## Differences

| **Area**                          | **Ubuntu**                                                      | **Solaris**                                                                                                          | **Key Differences**                                                                                                                                                     |
| --------------------------------- | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **System Information**            | `uname -a` (displays basic info like kernel name, hostname, OS) | `showrev -a` (displays detailed info including OS version, hardware type, patch level)                               | `uname` offers basic details; `showrev` provides comprehensive Solaris-specific information.                                                                            |
| **Package Installation**          | `sudo apt-get install <package>` (uses APT package manager)     | `pkgadd -d <package>` (uses Solaris Package Manager; sudo not required before Solaris 11)                            | Different package managers (Solaris uses the Solaris Package Manager (SPM)) and syntax; Solaris leverages RBAC for permissions (sudo supported from Solaris 11 onward). |
| **Permission Management**         | `chmod 700 filename``find / -perm 4000` (to find SUID files)    | `chmod 700 filename``find / -perm -4000` (to find SUID files)                                                        | The find command in Solaris uses a hyphen before the permission value, reflecting differences in the permission system.                                                 |
| **NFS Configuration**             | Mount with `mount -F nfs <server>:/nfs_share /mnt/local`        | Share a directory with `share -F nfs -o rw /export/home` and mount similarly; NFS config stored in `/etc/dfs/dfstab` | Solaris uses the `share` command to set up NFS shares and stores configurations in `/etc/dfs/dfstab`.                                                                   |
| **Process Mapping**               | `sudo lsof -c apache2` (lists files opened by a process)        | `pfiles \`pgrep httpd`` (lists files opened by a process)                                                            | Ubuntu uses `lsof` for process mapping; Solaris uses `pfiles` to achieve similar results.                                                                               |
| **Executable Access / Debugging** | `sudo strace -p \`pgrep apache2`` (traces system calls)         | `truss ls` (or similar commands to trace system calls, signals, and child processes)                                 | Solaris's `truss` can trace signals and child processes, while Ubuntu's `strace` is limited in these aspects.                                                           |


## References:

