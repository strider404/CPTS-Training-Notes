
2025-06-19 21:35

Tags: #network  

## Network Traffic Analysis

- **Network Traffic Analysis** is the process of *inspecting network traffic* to understand communications, establish a performance baseline, and identify anomalies

#### Key Applications of NTA
- **Real-time Threat Collection**: Capturing and analyzing live traffic to identify emerging threats.

- **Establishing Baselines**: Defining what constitutes normal day-to-day network communication to easily spot deviations.

- **Identifying Anomalies**: Detecting traffic from non-standard ports, suspicious hosts, and protocol errors (e.g., HTTP errors, TCP issues).

- **Malware Detection**: Identifying malware signatures, such as those from ransomware or exploits, as they traverse the network.

- **Forensics and Threat Hunting**: Aiding in the investigation of past security incidents and proactively searching for hidden adversaries.

#### Common Tools for NTA

- **Packet Sniffers (Command-Line)**:
	- `tcpdump`: A powerful command-line tool for capturing and interpreting network traffic.
	- `Tshark`: The command-line equivalent of Wireshark.
	- `NGrep`: A tool for applying pattern matching (like `grep`) to network packets.
	- `tcpick`: A sniffer that specializes in reassembling TCP streams.

- **Packet Sniffers (GUI)**:
	- `Wireshark`: A widely-used graphical analyzer for in-depth inspection of network traffic.

- **Traffic Capture Hardware**:
	- **Network Taps**: Devices that create a copy of network traffic to be sent to an analysis tool without altering the original flow.
	- **SPAN Ports (Port Mirroring)**: A feature on network switches to copy traffic from one or more ports to a designated analysis port.

- **Analysis Platforms**:
	- **SIEM (Security Information and Event Management)**: Systems like Splunk that aggregate, analyze, and visualize data from various sources.
	- **Elastic Stack**: A suite of tools for data ingestion, searching, and visualization.

- **Filtering Language**:
	- **Berkeley Packet Filter (BPF) Syntax**: A common filtering language used by many NTA tools to precisely select the traffic you wish to analyze.

#### The NTA Workflow

![[Pasted image 20250620214120.png]]

- **Ingest Traffic**:
	- *Capture* network traffic from a *chosen point* in the network (e.g., a specific VLAN, a server, or a backbone link).
	- Use capture *filters* if you have a pre-existing idea of what to look for to reduce the initial data volume.

- **Reduce Noise by Filtering**:
	- After the initial capture, apply display filters to *remove irrelevant traffic* (e.g., broadcast and multicast packets).
    - This step is critical for making large datasets manageable and focusing the analysis.

- **Analyze and Explore**:
	- Examine the filtered data for patterns and specific details relevant to your investigation.
	- *Key questions* to ask include:
	    - Is traffic encrypted when it should be (or unencrypted when it shouldn't be)?
	    - Are hosts attempting to access unauthorized resources?
	    - Are devices communicating that do not normally interact?

- **Detect and Alert**:
	- Based on the analysis, determine if the observed activity is *normal*, an *error*, or *malicious*.
    - Tools like an Intrusion Detection System (*IDS*) or Intrusion Prevention System (*IPS*) can be used here to automatically apply heuristics and signatures to detect known threats.

- **Fix and Monitor (Post-Cycle)**:
	- This is a crucial step that follows the main analysis loop.
	- After implementing a fix or mitigating a threat, you must continue to monitor the relevant network segments to verify that the issue has been resolved and has not created any new problems.

## References:

[Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/81/section/773)