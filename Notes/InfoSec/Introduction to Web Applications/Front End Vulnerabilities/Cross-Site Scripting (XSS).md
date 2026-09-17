
2025-07-23 15:47

Tags: #web  

## Cross-Site Scripting (XSS)

- **Definition**: Cross-Site Scripting (XSS) is a web security vulnerability that *allows an attacker to inject malicious JavaScript code* into web pages viewed by other users. It is an *advanced form of HTML Injection*.

- **Objective**: The primary goal is to *execute code on a victim's client-side* (browser) to potentially steal sensitive information, hijack user sessions, or gain control of their account.

- **Types of XSS**:
	- **Reflected XSS**: Occurs when user input is displayed on the page after processing (e.g., search result or error message).
	  
	- **Stored XSS**: The malicious script is permanently *stored on the target server*, such as in a database. It is then delivered to any user viewing the stored content (e.g., a forum post or a comment).
	  
	- **DOM-based XSS**: The vulnerability exists in the *client-side* code rather than the server-side code. The attack payload is executed as a result of modifying the Document Object Model (DOM) environment in the victim's browser.


## References:
https://academy.hackthebox.com/module/75/section/758
