
2026-05-15 15:08

Tags: #escalation  

## Docker

- **Definition:** An open-source platform providing a portable and consistent runtime environment for software applications.

- **Containers:** Lightweight, isolated environments running at the OS level. They share the host's file system and system resources, making them significantly more resource-efficient than traditional virtual machines.

## Architecture

- **Docker Daemon (Server):** The powerhouse that manages the heavy lifting. It handles the *creation, execution, and monitoring* of containers. It also manages image pulling/storing, resource utilization, networking (virtual networks, DNS), and persistent storage (volumes).


- **Docker Client:** The CLI interface used to *send commands to the Daemon* via a RESTful API or Unix socket.


- **Docker Compose:** An additional client tool that *orchestrates multi-container applications using a declarative YAML file*, managing dependencies, networking, and volumes simultaneously.


- **Docker Desktop:** A *GUI* application for MacOS, Windows, and Linux that simplifies container and resource management visually.

## Images vs. Containers

- **Docker Images:** *Read-only, immutable blueprints* containing everything needed to run an application (code, dependencies, configurations). They are typically built using a `Dockerfile`.


- **Docker Containers:** The *running, mutable instances of Docker images.* Each operates independently with its own filesystem and processes. Any changes made inside a container are lost when it stops, unless explicitly saved to a new image or a persistent volume.

## Privilege Escalation Vectors

- **Shared Directories (Volume Mounts):** Directories that bridge the host and container filesystems. If a container has access to sensitive host directories (e.g., a user's home folder), an attacker can extract private SSH keys (like `id_rsa`) or overwrite files to gain access to the host system.
	- ![[Pasted image 20260515151430.png]]


- **Docker Sockets (`docker.sock`):** The file that facilitates communication between the client and daemon. If this socket is writable by a standard user or improperly exposed, an attacker can use it to spawn a highly privileged container. By mapping the host's root directory (`/`) to the container (`-v /:/hostsystem`), they can gain full root access to the host.
	- ![[Pasted image 20260515151514.png]]
	- Upload a static [`docker`](https://master.dockerproject.com/linux/x86_64/docker) binary to the container if it isn't already installed, and use it to interact with the socket.
		- ![[Pasted image 20260515151532.png]]
	- Create a new, privileged container that mounts the host's root directory (`/`) to a folder inside the container (`/hostsystem`): `docker -H unix:///app/docker.sock run --rm -d --privileged -v /:/hostsystem main_app`
		- ![[Pasted image 20260515151607.png]]
	- Access the new container: `docker -H unix:///app/docker.sock exec -it <container_id> /bin/bash`
		- ![[Pasted image 20260515151616.png]]



- **Docker Group Membership / SUID:** Any user belonging to the `docker` group—or having `sudo`/SUID privileges for the Docker binary—has the authority to interact with the Docker daemon. This allows them to execute the same container-spawning techniques mentioned above to immediately escalate their privileges to root.
	- ![[Pasted image 20260515151644.png]]
	- `docker run -v /:/mnt --rm -it ubuntu chroot /mnt bash`
## References:

