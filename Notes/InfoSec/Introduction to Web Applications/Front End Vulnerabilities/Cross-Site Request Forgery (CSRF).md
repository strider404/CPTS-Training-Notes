
2025-07-23 16:19

Tags: #web  

## Cross-Site Request Forgery (CSRF)

- **CSRF** is a web application vulnerability where an attacker *tricks a victim's browser into making an unintended request* to a site where the victim is already authenticated.

- This allows the attacker to perform actions on behalf of the victim, such as **changing their password or making purchases.**

## Mechanism

- CSRF attacks can *leverage other vulnerabilities*, such as Cross-Site Scripting (XSS), by injecting malicious scripts.

- A typical scenario involves **crafting a JavaScript payload that automatically executes a sensitive action** (e.g., a password change API call) using the victim's active session cookie.

- The payload can be delivered through *various means*, such as a malicious link or a compromised page, and executes when the victim's browser processes it.

- Targeting **administrators** can lead to higher-privilege access and potential back-end server compromise.


#### Prevention and Mitigation

- **Input Filtering (General):**
	- **Sanitization:** *Remove potentially dangerous characters* from user input and from data before it is displayed to the client.
	  
	- **Validation:** Ensure all user-submitted data conforms to the *expected format* and type.

- **CSRF-Specific Defenses:**
	- **Anti-CSRF Tokens:** Implement unique, unpredictable tokens for each user session or sensitive request. The server validates this token before executing the action.
	  
	- **SameSite Cookie Attribute:** Use the `SameSite` cookie attribute (`Strict` or `Lax`) to control when a browser sends cookies with cross-origin requests.
	  
	- **Functional Protections:** Require user re-authentication (e.g., re-entering the password) for critical operations.


## References:
https://academy.hackthebox.com/module/75/section/828
