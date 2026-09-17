
2026-05-19 18:55

Tags: #escalation  

## Netfilter

- **Definition:** A core Linux kernel module (often called the "software layer") that controls and regulates network traffic.


- **Core Functions:**
    - Packet defragmentation
        
    - Connection tracking
        
    - Network address translation (NAT)


- **Mechanism:** It intercepts and manipulates incoming/outgoing IP packets using the hook mechanisms of the IPv4 and IPv6 stacks, executing actions via tools like `iptables` and `arptables`.


- **Environmental Risk:** Enterprise networks often run outdated kernels because updating underlying systems to match application dependencies is time-consuming.


- **Container Limitations:** While Docker and virtual machines provide isolation, they still share the underlying host kernel. A kernel vulnerability allows attackers to break out of the container and compromise the host.

## Notable Privilege Escalation Vulnerabilities

- **CVE-2021-22555 (Kernel 2.6 - 5.11)**
    - **Vector:** Out-of-bounds write.
        
    - **Exploitation:** Corrupts memory via message queues within a namespace sandbox.
        
    - **Execution:** The provided C exploit requires compilation with a 32-bit static flag (`gcc -m32 -static`).


- **CVE-2022-25636 (Kernel 5.4 - 5.6.10)**
    - **Vector:** Heap out-of-bounds write in `net/netfilter/nf_dup_netdev.c`.
        
    - **Exploitation:** Leaks `net_device` pointers and sprays the heap using `kmalloc` to overwrite security pointers and bypass KASLR.
        
    - **Opsec Warning:** Highly unstable. A failed exploit will likely corrupt the kernel, causing a crash that requires a full server reboot.


- **CVE-2023-32233 (Kernel up to 6.3.1)**
    - **Vector:** Use-After-Free (UAF) in `nf_tables`.
        
    - **Exploitation:** Abuses "anonymous sets" (temporary workspaces for batch requests). The kernel fails to clear these sets properly after use, allowing an attacker to interact with the corrupted kernel memory to obtain root.

## References:

