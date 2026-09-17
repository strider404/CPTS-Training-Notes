
2025-06-25 11:38

Tags: #network  

## Descriptive Analysis: Defining the Investigation

- **Goal:** To *describe* the data set and define the scope of the analysis.

- **Key Questions:**
	- What is the suspected issue (e.g., breach, network problem)?
	  
	- What is the scope (target hosts, network segments)? Example: `192.168.100.0/24`.
	  
	- What is the time frame? Example: Last 48 hours.
	  
	- What are the specific targets or indicators (e.g., malicious filenames like `superbad.exe`, protocols like HTTP/FTP)?

## Diagnostic Analysis: Finding the Cause

- **Goal:** To *clarify the causes and effects* of an event by examining data.

- **Steps:**
	- **Capture Traffic:** *Collect live traffic or pull historical data* (PCAP, netflow) from relevant network segments.
	  
	- **Filter Traffic:** *Remove irrelevant* data ("noise") and *baseline traffic* to isolate packets pertinent to the investigation.
	  
	- **Analyze Traffic:** Inspect the filtered data to understand what occurred. Examples include filtering for `ftp-data` to reconstruct transferred files or `http.request.method == "GET"` to find specific download requests.


## Predictive Analysis: Anticipating Future Events

- **Goal:** To use current and historical data to *identify trends and predict future* probabilities.

- **Actions:**
	- **Documentation:** Meticulously *log all findings*, including timestamps, suspicious hosts, and relevant packet numbers.
	  
	- **Summarization:** Create a clear, concise *summary* of the findings to enable superiors to make informed decisions (e.g., quarantining hosts, initiating incident response).


## Prescriptive Analysis: Recommending Solutions

- **Goal:** To *determine the necessary actions* to eliminate the current problem and prevent its recurrence.

- **Actions:**
	- **Prescribe Solutions:** Based on the analysis, recommend specific actions.
	  
	- **Document Lessons Learned:** Reflect on the entire process to strengthen future analysis and response procedures.
## References:

[Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/81/section/957)