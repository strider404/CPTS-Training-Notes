
2025-02-12 16:42

Tags:  #virtualization 

# Virtual machines

1. `Virtual machine (VM)` is a ==virtual operating system== that runs on a host system (an actual physical computer system). The VMs act independently of each other and do not influence each other.

2. The physical hardware resources of the host system are allocated via `hypervisors`. Hypervisor manages the hardware resources.

	Tức là cái app mà mình dùng để virtualization (Vmware) và nó sẽ quản lí tài nguyên hardware

3.  From the application perspective, an operating system installed within the VM ==behaves as if installed directly on the hardware.==

4. Performance < normal (because the virtualization layer also needs resources)

5. Cons:

![[Pasted image 20250212170105.png]]
# References:
[Setting Up](https://academy.hackthebox.com/module/87/section/881)
