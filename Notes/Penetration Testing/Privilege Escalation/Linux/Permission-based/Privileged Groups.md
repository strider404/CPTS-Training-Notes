
2026-05-13 16:04

Tags: #escalation  

## LXC / LXD Group

- **Concept:** LXD is *Ubuntu's container manager*. Members of the `lxd` group can create *privileged containers* to access the host's entire file system.


- **Exploitation Steps:**
    1. Verify group membership using the `id` command.
        1. ![[Pasted image 20260513215659.png]]
            
    2. Download and extract a lightweight OS image (like Alpine).
        1. ![[Pasted image 20260513215709.png]]
            
    3. Run `lxd init` and accept the default initialization prompts.
        1. ![[Pasted image 20260513215737.png]]
            
    4. Import the unzipped image into LXD using `lxc image import`.
        1. ![[Pasted image 20260513215745.png]]
            
    5. Initialize a new container with the flag `security.privileged=true`. This *removes UID mapping,* making the container's root user identical to the host's root user.
        1. ![[Pasted image 20260513215801.png]]
            
    6. Mount the root of the host file system (`/`) to a directory inside the container (e.g., `/mnt/root`) using `lxc config device add`.
        1. ![[Pasted image 20260513215925.png]]
            
    7. Start the container and spawn a shell (`lxc exec [container_name] /bin/sh`).
        1. ![[Pasted image 20260513215936.png]]


- **Impact:** Complete root access to the host file system, allowing you to read `/etc/shadow` or add root SSH keys.

## Docker Group

- **Concept:** Being in the `docker` group is practically equivalent to having passwordless root access to the host file system.


- **Exploitation:** Spawn a new Docker container while mounting a sensitive host directory as a volume.
    - _Example command:_ `docker run -v /root:/mnt -it ubuntu`


- **Impact:** Once inside the container, you can browse the mounted host directories to steal or plant root SSH keys, or read `/etc/shadow` for offline password cracking.

## Disk Group

- **Concept:** Members have full read/write access to block devices stored in `/dev`, including the main operating system drive (e.g., `/dev/sda1`).


- **Exploitation:** Attackers can bypass standard file system permissions by using tools like `debugfs` to interact directly with the raw disk device.


- **Impact:** Grants root-level visibility and access to the entire file system, allowing for the extraction of credentials, SSH keys, or the modification of files to add a privileged user.

## ADM Group

- **Concept:** Members are granted read access to all system logs stored within the `/var/log` directory.

- **Exploitation:** While this does not provide an immediate path to a root shell, it is highly valuable for reconnaissance.
  
- **Impact:** Attackers can read logs to find accidentally exposed sensitive data, track user behaviors, or enumerate hidden cron jobs that might be vulnerable to other privilege escalation techniques.
## References:

