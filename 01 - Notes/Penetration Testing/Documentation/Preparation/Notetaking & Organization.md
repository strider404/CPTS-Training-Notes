
2026-05-30 10:26

Tags: #documentation 

## Notetaking Structure

- **Administrative & Scoping:** Project manager contacts, Rules of Engagement (RoE), in-scope IPs/URLs, and client-provided credentials.
    
- **Attack Path:** A step-by-step outline (with commands and screenshots) of how you compromised a host or domain.
    
- **Research & Enumeration:** Dedicated sections for Vulnerability Scans, Service Enumeration, Web Applications, Active Directory, and OSINT. Track both successes and failures to avoid repeating work.
    
- **Findings:** A dedicated folder/section for each discovered vulnerability, combining your narrative with specific evidence.
    
- **Logs:** * **Activity Log:** High-level timeline of your actions (useful for client event correlation).
    - **Payload Log:** Track what payloads were used, their file hashes, upload locations on the target, and cleanup status.
        
    - **Credentials:** A centralized vault for compromised hashes and cleartext passwords.

## Tooling and Data Security

- Choosing a notetaking tool is a matter of personal preference, but **data security is not**.
	- Cloud solutions (Evernote, Notion) are fine for CTFs, but client data often legally requires local storage. Always check your company's data policies.
	    
	- **Obsidian** is highly recommended because it stores files locally in Markdown, allowing you to seamlessly integrate your physical folder structure with your notetaking app.

## Logging & Evidence Collection

- If you are working in a terminal, you should be logging it. **Tmux** , paired with the `tmux-logging` plugin, is an industry standard. It prevents the embarrassing situation of being unable to provide evidence to a client.

- **Key Tmux Shortcuts:**
	- `Prefix + [Shift] + [I]`: Install plugins.
	    
	- `Prefix + [Shift] + [P]`: Toggle logging for the current pane.
    
	- `Prefix + [Alt] + [Shift] + [P]`: Retroactive logging (saves the scrollback buffer). _Tip: Increase your `history-limit` in `.tmux.conf` so you don't lose early data._
    
	- `Prefix + [Alt] + [P]`: Screen capture a single pane (prevents messy text copying when using split panes).


## Evidence Formatting & Redaction

- Clients need clear, reproducible evidence. Your goal is to make it as easy as possible for their internal teams to understand and fix the issue.
  
- **Terminal Text > Screenshots:** Whenever possible, copy terminal output directly into your report as formatted text. It is easier to redact, highlights cleanly, keeps file sizes down, and allows the client to copy/paste your commands. Use `<SNIP>` to remove unnecessary walls of text.

- **Highlighting:** Use color-coding in your report (e.g., blue for the command run, red for the successful output) to guide the reader's eye.
  
  
- **CRITICAL REDACTION RULE:** Never use blurring or pixelation to redact sensitive data (credentials, PII) in screenshots. Tools like _Unredacter_ can reverse this effect. **Always use solid shapes (like black bars) applied directly to the image file**, not just overlaid in Microsoft Word where they can be deleted.


## What NOT to Capture

- "Do no harm" extends to data handling. Do not extract or archive raw **Personally Identifiable Information (PII)** or **legally sensitive documents** from the client's network. If you gain access to a sensitive network share, take a screenshot of the **directory listing** (the file names alone prove access) rather than opening and downloading the sensitive files, which could trigger massive compliance liabilities like GDPR.


## Recommended Folder Structure

|**Parent Directory**|**Sub-Directories & Purpose**|
|---|---|
|**Admin**|Scope of Work (SoW), kickoff notes, status reports.|
|**Deliverables**|Draft reports, slide decks, supplemental spreadsheets.|
|**Evidence**|Contains the core data of the assessment.|
|_Evidence Subfolders_|**Findings:** A dedicated folder for each vulnerability.<br><br>  <br><br>**Scans:** Subfolders for AD, Service, Vuln, and Web scan outputs.<br><br>  <br><br>**Notes:** Your markdown files or tool databases.<br><br>  <br><br>**OSINT:** Output from tools like Maltego.<br><br>  <br><br>**Logging Output:** Tmux and Metasploit logs.<br><br>  <br><br>**Misc Files:** Payloads, web shells, and custom scripts.|
|**Retest (Optional)**|Mirrored folder structure for validation testing later on.|
## References:

