
2026-06-01 10:48

Tags: #documentation 

## Templates and MS Word Mastery

- Never reinvent the wheel, and never overwrite a previous client's report (this is a massive operational security risk). Always start with a fresh, blank template tailored to the assessment type.

- If you are using Microsoft Word, **use Word for Windows**. Word for Mac lacks critical features like the VB Editor for macros and handles PDFs poorly.

- **Essential MS Word Practices:**
	- **Use Styles:** Rely on Font and Table Styles instead of manual/direct formatting. If you need to change a heading's look, changing the Style updates the entire document instantly.
	    
	- **Use Built-in Captions:** Right-click to caption images and tables. Word will automatically renumber them if you add or delete a figure later.
	    
	- **Language Settings:** Set your terminal/code block Font Style to "ignore spelling and grammar" so your spellchecker doesn't flag every Linux command.
	    
	- **Bookmarks:** Use these to mark sections for internal hyperlinks or for macros to automatically delete irrelevant sections.

- Useful Word Hotkeys

|**Hotkey**|**Function**|
|---|---|
|**F4**|Repeats your last action (great for applying styles multiple times).|
|**Ctrl+A $\rightarrow$ F9**|Selects everything and updates all fields, including the Table of Contents.|
|**Ctrl+Alt+S**|Splits the Word window into two panes to view different sections simultaneously.|
|**Shift+F5**|Moves the cursor back to the exact spot of your last edit.|
## Automation and Tooling

- If you don't have a dedicated reporting platform, use Word macros (`.dotm` files) to automate repetitive tasks. Macros can trigger pop-ups asking for the client's name and scope, instantly populating placeholders throughout the document.

- Eventually, you should adopt a **Findings Database** or reporting tool (e.g., Ghostwriter, PlexTrac, WriteHat, Dradis). Maintaining a centralized database of sanitized, pre-written findings ensures consistency across your team and saves countless hours of rewriting standard vulnerabilities.

## Polish and Professionalism

- Your report is your highlight reel. You could execute the most brilliant exploit chain in history, but if it looks terrible on paper, the client won't see the value.

- **Tell a Story:** Don't just dump screenshots. Explain the narrative of the attack and why it matters to the business.
    
- **Sanitize Evidence:** Use tools like Greenshot to draw solid boxes (never blur) over sensitive data like cleartext passwords or hashes.
    
- **Clean Up Tool Output:** Redact unprofessional terminal outputs (like the "Pwn3d!" in CrackMapExec) and ensure your terminal prompt is professional (e.g., no crude hostnames).
    
- **Check Wordlists:** Ensure your Hashcat output doesn't accidentally include crude or offensive cracked passwords from your wordlist.
    
- **Annotate Screenshots:** A screenshot is useless if the reader doesn't know what to look at. Add arrows or boxes to draw the eye to the payload or impact.

## Client Communication

- **Start/Stop Notifications:** Send daily emails stating when testing begins and ends. Include your attack IP so the client's SOC can distinguish your traffic from real threats.
    
- **Real-Time Alerts:** Do not wait for the final report to notify the client of critical issues (e.g., RCE, Domain Admin compromise, or if a host goes down).
    
- **Keep Receipts:** Maintain flawless scanner logs and command histories. If a client blames you for a network outage, you need concrete proof of exactly what you were doing at that exact time.

## Quality Assurance (QA) and Delivery

- **Never QA Your Own Work:** Always have at least one (preferably two) other people review your report. If you work alone, sleep on it and review it the next day with fresh eyes.
    
- **Use a Checklist:** Standardize the QA process so reviewers are checking for the same formatting, grammar, and technical accuracy issues every time.
    
- **Draft vs. Final:** Issue the report as a "Draft" first. Hold a **Report Review Meeting** to walk the client through the findings and answer their questions. Once they accept the report, issue the "Final" version.
## References:

