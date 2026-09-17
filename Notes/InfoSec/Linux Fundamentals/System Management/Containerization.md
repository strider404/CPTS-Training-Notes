
2025-03-01 09:24

Tags: #linux  #virtualization  

## Containerization

- Containerization: packaging and running applications separately 

- Containers share the same kernel & resources

- Containers vs VMs: 
	- Much more light-weight
	- Share the same kernel
	- The level of isolation is lower -> can have more security risks
	- VMs is like creating a whole new stage for a band to perform, while containers only take what each band needs to use on 1 stage


## Dockers

- Docker: open-source automating software deployment program, has a layer of isolation between containers

- Imagine Docker containers as a sealed lunchbox. You can eat the food (run applications) inside, but once you close the box (stop the container), everything resets. To make a new lunchbox (new container) with updated contents (modified configurations), you create a new recipe (Dockerfile) based on the original. When serving multiple lunchboxes in a restaurant (production), you'd use a kitchen system (Kubernetes/Docker Compose) to manage all the orders smoothly.

- Docker need ==image== to operate (a snapshot of software & all its dependencies to the OS level). Obtain Docker images from [Docker Hub](https://hub.docker.com/)

- Images created by Dockerfile (code to tell Docker how to build an image)

- Dockerfile example: 

![[Pasted image 20250301101917.png]]


- Docker Build: `docker build -t FS_docker .`

- Docker Run: `docker run -p <host port>:<docker port> -d <docker container name>`

- Changes to Docker images ==won't be saved==, u must create new image based on the old image by creating new Dockerfile with the FROM statement (specifying the base image), specify the changes & build again

- Changes inside the container are removed after closing it

- Docker management: 

| Command        | Description                   |
| -------------- | ----------------------------- |
| docker ps      | List all running containers   |
| docker stop    | List all running containers   |
| docker start   | Start a stopped container.    |
| docker restart | Restart a running container.  |
| docker rm      | Restart a running container.  |
| docker rmi     | Remove a Docker image.        |
| docker rmi     | View the logs of a container. |

- Create a file hosting container using Docker, see in the HTB section below


## Linux Containers

- Linux Containers (LXC): virtualization technology allow multiple Linux systems (containers) run on ==single host==

- LXC vs Docker

| Category       | Description                                                                                                                                                                                                                                                                              |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Approach       | LXC focuses on system-level containerization tools, create a isolated Linux environment, act like a lightweight VM<br>Docker focuses on application containers                                                                                                                           |
| Image building | Docker uses a standardized image format (Docker images) that includes everything needed to run an application (code, libraries, configurations). <br>LXC requires more manual setup for building and managing environments.                                                              |
| Portability    | Docker's container images can be easily shared across different systems via Docker Hub or other registries. <br>LXC environments are less portable as they are more tightly integrated with the host system’s configuration.                                                             |
| Easy of use    | Docker offer a user-friendly CLI and extensive community support. <br>LXC require more in-depth knowledge of Linux system administration, making it less straightforward for beginners.                                                                                                  |
| Security       | Docker containers are generally more secure thanks to additional isolation layers like AppArmor and SELinux, along with its read-only filesystem feature. <br>LXC containers, while secure, may need additional configurations to match the level of isolation Docker offers by default. |

- Creating an LXC Container: `sudo lxc-create -n linuxcontainer -t ubuntu` (container named linuxcontainer)

- Managing LXC Containers:

| Command                                                                                             | Description                                                    |
| --------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| `lxc-ls`                                                                                            | List all existing containers                                   |
| `lxc-stop -n <container>`                                                                           | Stop a running container.                                      |
| `lxc-start -n <container>`                                                                          | Start a stopped container.                                     |
| `lxc-restart -n <container>`                                                                        | Restart a running container.                                   |
| `lxc-config -n <container name> -s storage`                                                         | Manage container storage                                       |
| `lxc-config -n <container name> -s network`<br><br>`sudo nano /var/lib/lxc/<container_name>/config` | Manage container network settings                              |
| `lxc-config -n <container name> -s security`                                                        | Manage container security settings                             |
| `lxc-attach -n <container>`                                                                         | Connect to a container.                                        |
| `lxc-attach -n <container> -f /path/to/share`                                                       | Connect to a container and share a specific directory or file. |
| `lxc-destroy --name mycontainer`                                                                    | Destroy a container                                            |

### Securing LXC

 - To limit resources of the container, need to change the ==cgroups== variables

- Config the configuration file of the container `sudo vim /usr/share/lxc/config/linuxcontainer.conf`

![[Pasted image 20250301111202.png]]

- lxc.cgroup.cpu.shares: CPU time that can be used by the container (default 1024), if we set it 512, it will only have half the CPU time

- lxc.cgroup.memory.limit_in_bytes: set maximum memory a container can use

- After configuration, restart: `sudo systemctl restart lxc.service`

- Namespace: feature that provides the abstraction of system resources for isolation 

- Each container has different process ID (pid), network interfaces, routing tables, firewall rules and most importantly, root file system (mnt) from the host -> any changes in container won't affect the host -> more secured (provided by namespace)


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2097)