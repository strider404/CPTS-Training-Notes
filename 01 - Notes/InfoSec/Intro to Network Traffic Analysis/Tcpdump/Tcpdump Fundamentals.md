
2025-06-25 15:43

Tags: #network #hands-on 

## Tcpdump

- **Definition**: A *command-line packet sniffing tool* for Unix-like operating systems.
  
- **Functionality**: *Captures and analyzes network traffic* directly from a network interface or a saved file.
  
- **Technology**: Utilizes `pcap`/`libpcap` libraries and places the network interface in promiscuous mode to capture all local network traffic.
  
- **Privileges**: Requires *root* or *administrator* privileges (i.e., must be run with `sudo`).
  
- **Windows Alternative**: The original Windows port, `WinDump`, is no longer supported. The recommended alternative is to use `tcpdump` within the Windows Subsystem for Linux (WSL).

#### Basic Capture Options

- **Interface Selection**:
    - `-D`: *Lists* all available network interfaces for capture.
      
    - `-i <interface>`: *Specifies the network interface* to listen on (e.g., `-i eth0`).


- **Output Formatting**:
    - `-n`: *Prevents* the resolution of IP *addresses* to *hostnames*.
      
    - `-nn`: *Prevents* the resolution of both *IP addresses and port numbers*.
      
    - `-e`: Includes the *Ethernet (Data Link layer)* *header* in the output, showing *MAC addresses*.
        - **Note**: The Source & Destination MAC will be displayed in the reverse order
          
    - `-v, -vv, -vvv`: *Increases* the level of *detail* (verbosity) in the output.
      
    - `-X`: *Displays the content* of packets in both *hexadecimal* and *ASCII* formats.
      
    - `-XX`: Same as `-X` but also includes the *Ethernet header*.
      
    - `-S`: Display sequence number in *absolute value*
      
    - `-A`: Displays the packet content in *ASCII*


- **Capture Control**:
    - `-c <number>`: Captures a *specific number of packets* and then exits.
      
    - `-s <bytes>`: Sets the "*snapshot length*," which is the amount of data to capture from each packet.


- **File Operations**:
    - `-w <filename.pcap>`: *Writes* the raw packet capture to a specified file. This does not print output to the terminal.
      
    - `-r <filename.pcap>`: *Reads* and displays packet data from a specified file. Switches can be used to format the output from the file.
      
    - `-l`: *Pipe* the contents of a .pcap file to another command

#### Tcpdump Output

![[Pasted image 20250625163942.png]]

- **Timestamp**: The time the packet was captured.
  
- **Protocol**: The network protocol (e.g., `IP`).
  
- **Source & Destination**: The source and destination IP addresses and port numbers (e.g., `172.16.146.2.55260 > 172.67.1.1.https`).
  
- **Flags**: TCP control flags, such as `[S]` (SYN), `[P]` (PSH), `[F]` (FIN), and `[.]` (ACK).
  
- **Sequence/Acknowledgement Numbers**: Values used by TCP to ensure reliable data transmission.
  
- **Protocol Options**: Additional parameters like window size or timestamps.

- **Notes**: Additional info

#### Live-time Output

![[Pasted image 20250626105838.png]]

- **Timestamp**
- **Ethernet header (Layer 2)**: from 00:50.... to length 60
- **IP header:** from (tos 0x0,...) to the Destination IP (192.168.208.128)
- **TCP header:** from Flags: [S.] to Length 0, the port numbers is included in the IP Addresses
- **Payload**
## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/81/section/774)