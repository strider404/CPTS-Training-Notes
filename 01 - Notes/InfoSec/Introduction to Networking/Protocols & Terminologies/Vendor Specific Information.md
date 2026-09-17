
2025-06-05 10:24

Tags: #network  

## Cisco IOS

- **Definition**: The *operating system* for Cisco network devices *(routers, switches),* providing features for network management and operation.

- **Key Features**:
	- IPv6 support
	- Quality of Service (QoS)
	- Security features (encryption, authentication)
	- Virtualization (VPLS, VRF)

- **Management Methods**:
    - Command Line Interface (CLI)
    - Graphical User Interface (GUI)

- **Supported Protocols & Services**:
	- **Routing Protocols**: OSPF, BGP
	- **Switching Protocols**: VLAN Trunking Protocol (VTP), Spanning Tree Protocol (STP)
	- **Network Services**: Dynamic Host Configuration Protocol (DHCP)
	- **Security Features**: Access Control Lists (ACLs)

- **Password Types**:
    - **User**: For login, restricts access to device features.
    - **Enable Password**: For "enable" mode (advanced functions).
    - **Secret**: Secures access to specific functions/services (e.g., remote management).
    - **Enable Secret**: Extra-secure, encrypted password for "enable" mode.

- **Remote Access**: Configurable for SSH or Telnet, identifiable by "User Access Verification" message.


## VLANs

- **VLAN (Virtual Local Area Networks)**: Logical grouping of network endpoints on a switch, *segmenting* networks into *broadcast* domains.
	- Instead of using multiple physical switches for each department, we can *divide 1 switch*. Each "virtual partition" becomes a *separate, independent network*
	- Broadcast (send to all) domains is like if you shout in 1 room, the other won't hear it

- **Benefits**:
	- **Better Organization**: Grouping endpoints by attributes.
	- **Increased Security**: Prevents unauthorized sniffing between VLANs.
	- **Simplified Administration**: Independent of physical location.
	- **Increased Performance**: Reduces broadcast traffic, freeing bandwidth.

- Example:
![[Pasted image 20250605110244.png]]

- **VLAN IDs**:
	- **Range**: 1-4094 (0 and 4095 reserved).
	- **Normal-range**: 1-1005 (*VLAN 1* is default - should not alter, 1002-1005 reserved).
	- **Extended-range**: 1006-4094.
	- **Storage**: Normal-range customizations saved in `vlan.dat`; extended-range are not.

- **VLAN Memberships**:
    - **Static**: *Manual* assignment of *switch ports to a VLAN* (most common, more secure).
    - **Dynamic**: *Automatic* determination based on *MAC addresses* or protocols (e.g., VMPS), increases administrative overhead, less secure against MAC spoofing.

- **Port Types**:
	- **Access Ports**: Carry traffic of only one VLAN.
	- **Trunk Ports**: Carry traffic of multiple VLANs, connect different switches/routers.

#### VLAN Identification

- **Ethernet frame**: encapsulate data, provide addressing for local network communication *(using MAC addresses)*, and ensure data integrity during transmission within a local area network.
	- Operates at *Layer 2* of OSI Model
	- While the IP header operates at *Layer 3*
	- This acts like an outer envelope of a letter

- **Inter-Switch Link (ISL)**: Cisco-proprietary, *deprecated*, *encapsulates entire Ethernet frame*.

- **IEEE 802.1Q**: Industry standard, modifies Ethernet frame by adding a *4-byte header (TPID, TCI).*
	- **TPID (Tag Protocol Identifier)**: 2 bytes, Identifies 802.1Q-tagged frame (0x8100).
	- **TCI (Tag Control Information)**: Contains PCP, DEI, and VID.
	- **VID (VLAN Identifier)**: 12 bits, allowing 4094 (2^12) VLANs.
	- **Double Tagging**: Inserting multiple 802.1Q tags (802.1ad).
		- Why: because big network (like an ISP) also uses VLANs, you (or your company) use VLANs too, need 2 tags 1 for that big network and 1 for your VLAN, prevent conflict from each others 

![[Pasted image 20250605112944.png]]

- **VLAN-Capable NICs**:
	- **Linux**: VLANs created as sub-interfaces (e.g., `eth0.20`), using `modprobe 8021q`, `vconfig add`, or `ip link add`.
	- **Windows**: Configurable via Device Manager (VLAN ID property) or PowerShell (`Set-NetAdapter -VlanID`).
	- Details in the link

- **Analyzing VLAN Tagged Traffic**:
	- **Wireshark**: Use filters `vlan` or `vlan.id == [ID]`.
	- **Tshark**: Enumerate VLAN IDs with `tshark -r [file] -T fields -e vlan.id`.


#### Security Implications and VLAN Attacks

- **VLAN Hopping**:
	- **Mechanism**: Exploits Cisco's Dynamic Trunking Protocol (DTP). An attacker *mimics a switch* to form a *trunk link* (above), gaining access to all VLAN traffic.
	- **Tool**: Yersinia.

- **Double-tagging VLAN Hopping**:
	- **Mechanism**: Attacker embeds a *hidden 802.1Q tag inside an already tagged frame*. Works when the outer tag's *VLAN ID* matches the trunk port's native VLAN, causing the *second switch to forward based on the inner (malicious) tag.*
	- **Tools**: Scapy, Yersinia.

#### VXLAN (Virtual eXtensible Local Area Network)

- **Purpose**: Addresses VLAN limitations (4094 VLANs, STP link blocking) for large-scale data centers and cloud environments.
- **Nature**: Layer 2 overlay scheme on a Layer 3 network.
- **Identification**: VXLAN Network Identifier (VNI), a 24-bit segment ID, allowing 16 million VXLAN segments.
- **Benefits**: Scalability and flexibility for virtualized environments.


#### Cisco Discovery Protocol (CDP)

- **Function**: Cisco Layer 2 protocol for discovering information about directly connected Cisco devices (topology, management, troubleshooting).
- **Information Gathered**: Device ID, IP address, port ID, capabilities (e.g., Router), IOS version, platform.
- **Security Note**: Can be disabled if not needed for security reasons.


#### Spanning Tree Protocol (STP)

- **Function**: Network protocol preventing loops in networks with redundant switch connections, ensuring loop-free topology.
- **Information in Messages**: Root switch ID, MAC address, port ID, configuration parameters (max-age, hello-time, forward-delay).

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1878)
