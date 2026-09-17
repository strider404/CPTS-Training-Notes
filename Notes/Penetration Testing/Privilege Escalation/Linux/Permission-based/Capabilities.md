
2026-05-14 14:28

Tags:  #escalation 

## Capabilities

- **Linux capabilities grant specific, fine-grained privileges to processes**, moving away from the traditional all-or-nothing Unix user/group model.


- They enhance security by adhering to the principle of least privilege.


- Capabilities act as an alternative attack vector for privilege escalation if granted to poorly isolated, unsandboxed, or unnecessary processes.

## Managing Capabilities

- The `setcap` utility *assigns capabilities* to specific binaries.
	- ![[Pasted image 20260514144109.png]]


- Applying a capability allows a binary to **perform restricted actions**, like binding to network ports without being the root user.


- Example of setting a capability: `sudo setcap cap_net_bind_service=+ep /usr/bin/vim.basic`

## Capability Values and Flags

|**Value**|**Description**|
|---|---|
|`=`|Sets the capability but grants no privileges; useful for clearing previously set capabilities.|
|`+ep`|Grants Effective and Permitted privileges; allows the binary to perform the action but prevents inheritance.|
|`+ei`|Grants Effective and Inheritable privileges; child processes spawned by the executable inherit the capability.|
|`+p`|Grants Permitted privileges only; allows the action but prevents both inheritance and immediate effective use until explicitly requested.|

## High-Value Capabilities for Privilege Escalation

| **Capability**         | **Security Implication**                                                               |
| ---------------------- | -------------------------------------------------------------------------------------- |
| `cap_setuid`           | Allows setting the effective user ID, enabling a jump to the `root` user.              |
| `cap_setgid`           | Allows setting the effective group ID, enabling a jump to the `root` group.            |
| `cap_sys_admin`        | Grants broad administrative privileges (modifying system files, mounting filesystems). |
| `cap_dac_override`     | Bypasses all file read, write, and execute permission checks.                          |
| `cap_sys_chroot`       | Allows changing the root directory (`chroot`), bypassing file restrictions.            |
| `cap_sys_ptrace`       | Allows debugging and attaching to other processes to steal memory/secrets.             |
| `cap_sys_nice`         | Modifies process priorities, potentially leading to resource manipulation.             |
| `cap_sys_time`         | Modifies the system clock, disrupting timestamps or process scheduling.                |
| `cap_sys_resource`     | Modifies system resource limits (e.g., memory allocation, file descriptors).           |
| `cap_sys_module`       | Allows loading/unloading of kernel modules for deep system compromise.                 |
| `cap_net_bind_service` | Binds to privileged network ports to intercept or spoof traffic.                       |

## Enumerating Capabilities

- Searching for explicitly set capabilities across standard binary directories is a crucial enumeration step.


- Use the following command to **find and list all capabilities** on a target system:
	- `find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;`
	- ![[Pasted image 20260514145724.png]]


## Exploitation Example (`cap_dac_override`)

- Discovering `cap_dac_override` on a text editor (like `vim.basic`) allows for **arbitrary file modification** regardless of file ownership.


- The capability can be verified using: `getcap /usr/bin/vim.basic`
	- ![[Pasted image 20260514145854.png]]


- The attacker can leverage this text editor to target the `/etc/passwd` file.


- Interactive exploitation involves opening the file and manually removing the `x` (password requirement indicator) from the root user's line.
	- ![[Pasted image 20260514145958.png]]
	- ![[Pasted image 20260514150012.png]]


- Non-interactive exploitation can be executed in a single command using vim's script mode:
	- `echo -e ':%s/^root:[^:]*:/root::/\nwq!' | /usr/bin/vim.basic -es /etc/passwd`


- Once the `x` is removed from `/etc/passwd`, the attacker can escalate to root without a password using the `su` command.
## References:



