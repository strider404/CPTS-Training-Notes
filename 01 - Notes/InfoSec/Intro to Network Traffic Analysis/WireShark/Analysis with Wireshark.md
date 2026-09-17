
2025-07-01 11:42

Tags: #network #hands-on 

## Wireshark

- **Definition**: A free, open-source network traffic analyzer with a *graphical user interface (GUI)* used for *deep packet inspection*.

#### TShark

- A *command-line (CLI)* based version of Wireshark, suitable for systems without a GUI or for scripting

- **Basic TShark Switches (pretty similar to tcpdump):**

| **Switch Command** | **Result**                                                                                                          |
| :----------------: | ------------------------------------------------------------------------------------------------------------------- |
|         D          | Will display any interfaces available to capture from and then exit out.                                            |
|         L          | Will list the Link-layer mediums you can capture from and then exit out. (ethernet as an example)                   |
|         i          | choose an interface to capture from. (-i eth0)                                                                      |
|         f          | packet *filter* in libpcap syntax. Used during capture. (sudo tshark -i eth0 -f "host 172.16.146.2")                |
|         c          | Grab a specific number of packets, then quit the program. Defines a stop condition.                                 |
|         a          | Defines an *autostop condition*. Can be after a duration, specific file size, or after a certain number of packets. |
|   r (pcap-file)    | Read from a file.                                                                                                   |
|   W (pcap-file)    | Write into a file using the pcapng format.                                                                          |
|         P          | Will print the *packet summary* while writing into a file (-W)                                                      |
|         x          | will add Hex and ASCII output into the capture.                                                                     |
|         h          | See the help menu                                                                                                   |

#### Termshark

- A *terminal-based user interface (TUI)* that provides a Wireshark-like layout directly in the terminal.

## Wireshark GUI Walkthrough

![[Pasted image 20250701115927.png]]


- **Packet List (orange)**: A summary view of all captured packets in chronological order.

- **Packet Details (blue)**: A detailed, hierarchical view of the protocols and fields following the typical OSI Model (reverse order)

- **Packet Bytes**: The raw packet data displayed in hexadecimal and ASCII formats.

#### Filtering in Wireshark

- **Capture Filters**:
	- Applied _before_ the capture starts to limit the data being recorded.
	- Tab Capture -> Capture Filter

|**Capture Filters**|**Result**|
|:-:|---|
|host x.x.x.x|Capture only traffic pertaining to a certain host|
|net x.x.x.x/24|Capture traffic to or from a specific network (using slash notation to specify the mask)|
|src/dst net x.x.x.x/24|Using src or dst net will only capture traffic sourcing from the specified network or destined to the target network|
|port #|will filter out all traffic except the port you specify|
|not port #|will capture everything except the port specified|
|port # and #|AND will concatenate your specified ports|
|portrange x-x|portrange will grab traffic from all ports within the range only|
|ip / ether / tcp|These filters will only grab traffic from specified protocol headers.|
|broadcast / multicast / unicast|Grabs a specific type of traffic. one to one, one to many, or one to all.|

- **Display Filters**:
	- Applied _during or after_ the capture to analyze the collected data.
	- Tab Analyze -> Display Filter

|        **Display Filters**        | **Result**                                                                                    |
| :-------------------------------: | --------------------------------------------------------------------------------------------- |
|        ip.addr == x.x.x.x         | Capture only traffic pertaining to a certain host. This is an OR statement.                   |
|       ip.addr == x.x.x.x/24       | Capture traffic pertaining to a specific network. This is an OR statement.                    |
|       ip.src/dst == x.x.x.x       | Capture traffic to or from a specific host                                                    |
| dns / tcp / ftp / arp / ip / http | filter traffic by a specific protocol. There are many more options.                           |
|           tcp.port == x           | filter by a specific tcp port.                                                                |
|     tcp.port / udp.port != x      | will capture everything except the port specified                                             |
|          and / or / not           | AND will concatenate, OR will find either of two options, NOT will exclude your input option. |


## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/81/section/775)
