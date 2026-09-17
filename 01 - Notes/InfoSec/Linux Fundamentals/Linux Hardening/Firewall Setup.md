
2025-03-08 08:18

Tags: #linux #firewall 

## Firewall Setup

- Firewall: a virtual barrier monitor and control network traffic between different segments -> protect the system against security threats and malicious acts

- In Linux: manage the built-in firewall through kernel-level Netfilter framework

- iptable: born in 2000, allow users to use command-line based method to configure the IP address, ports, protocols filtering rules

- iptable is the rules, while Netfilter does the job

- Some alternatives for iptable:
	- nftables
	- UFW
	- FirewallD
## iptable

- Components of iptable:
	- Table: Organize and categorize rules based on the types of traffic 
	- Chains: Group of rules apply for specific stages
	- Rules: filtering criteria, actions take when the criteria is met (Rules = matches + target)
	- Matches: conditions for triggering the rules
	- Target: actions do when matches

### Table

- Primary tables:
	- Filter: general traffic filtering (built-in chains: INPUT, OUTPUT, FORWARD)
	- NAT: to modify source or destination addresses (built-in chains: PREROUTING, POSTROUTING).
	- Mangle: to modify packet header fields (built-in chains: PREROUTING, OUTPUT, INPUT, FORWARD, POSTROUTING).
	- Raw: for special packet processing options (with PREROUTING and OUTPUT chains).


### Chains

- Can be built-in (already exist with the tables) or user-define (to organize rules by criteria such as server groups or destination ports.)

- Some built-in chains

| Chain       | Description                                                                                     |
| ----------- | ----------------------------------------------------------------------------------------------- |
| INPUT       | filter incoming traffic.                                                                        |
| OUTPUT      | filter outgoing traffic.                                                                        |
| FORWARD     | Manages packets that are routed between different network interfaces; used for transit traffic. |
| PREROUTING  | modify the destination IP address of incoming packets before the routing table processes them   |
| POSTROUTING | modify the source IP address of outgoing packets after the routing table has processed them     |


- Ex: we can group all traffic to port 80 to a self-defined chain (HTTP for example) then apply rules for that chain (might use the -N command to create, and -j to forward the traffic)

### Rules & Matches & Target 

- Use the -A option to ==apply rules to a chain==

- Matches can match IP addresses, port numbers, protocol types, often use the -m options

- Some common matches:
![[Pasted image 20250308091125.png]]

- Targets: actions to take, may use the -j option

| Target (Action) | Description                                                                                   |
| --------------- | --------------------------------------------------------------------------------------------- |
| `ACCEPT`        | Permits the packet to proceed to its destination.                                             |
| `DROP`          | Silently blocks the packet without notifying the sender.                                      |
| `REJECT`        | Blocks the packet and sends an error message to the sender.                                   |
| `LOG`           | Records packet details in the system log.                                                     |
| `SNAT`          | Modifies the source IP address of the packet (used for outbound NAT).                         |
| `DNAT`          | Modifies the destination IP address of the packet (used for inbound NAT).                     |
| `MASQUERADE`    | Similar to SNAT but dynamically assigns the source IP (commonly used in NAT for dynamic IPs). |
| `REDIRECT`      | Reroutes packets to another port or IP address on the same machine.                           |
| `MARK`          | Tags packets for advanced processing, such as routing decisions.                              |

- Ex: `sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT`


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2099)