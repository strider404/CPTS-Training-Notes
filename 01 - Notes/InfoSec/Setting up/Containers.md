
2025-02-12 17:12

Tags: #virtualization   

# Containers

1. `Container`: an isolated group of `processes` running on a single host that corresponds to a complete application, including its configuration and dependencies. (application virtualization)

	Là 1 nhóm các tiến trình chạy cô lập với nhau, sử dụng chung 1 OS gốc, chứ ko tạo ra cả CPU ảo, GPU ảo, RAM ảo,... như VM

2. VM vs Container:
![[Pasted image 20250213154947.png]]

| VM                                                                 | Container                                                               |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| Applications & complete OS                                         | Application & only necessary OS components (libraries / binaries)       |
| Hypervisor (VMWare)                                                | OS with container engine                                                |
| Multiple VMs run in isolation from each other on a physical server | Several containers run isolated from each other on one operating system |

3.  `Linux Container Daemon` (`LXD`)  configured and controlled containers through commands

4.  An ==image== of the file system forms the basis of each container.
# Introduction to Docker

5. [Docker](https://www.docker.com/get-started) is open-source software that can isolate applications in containers, similar to operating system virtualization.
	-> applications can be transported and installed easily

6. Commonly run on Linux, but can be used in Windows via VM

7. [Docker Engine](https://docs.docker.com/engine/) is the main component of container virtualization.


# Introduction to Vagrant

8. [Vagrant](https://www.vagrantup.com/) is a tool that can create, configure and manage virtual machines or virtual machine environments.

9. VMs is created by code in Vagrantfile.

10. Used to create, provision, delete VMs

![[Pasted image 20250213162023.png]]
# References:

[Setting Up](https://academy.hackthebox.com/module/87/section/882)