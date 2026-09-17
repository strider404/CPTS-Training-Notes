
2025-07-23 11:15

Tags: #web  

## HTML Injection

- **Definition**: HTML Injection is a vulnerability that occurs when an application *accepts unfiltered user input* and *displays* it on the web page. This allows an attacker's input to be rendered as actual HTML code by the browser.
	- **Example**: input `<h1>WTF</h1>` will display WTF on the browser

- **Cause**: The root cause is the *failure* to validate and sanitize user input. This process should occur on *both the front-end (client-side) and back-end (server-side)*, as some input may be processed entirely on the front end without reaching the server.

- **Attack Vectors**:
    - **Direct Display**: JavaScript can take user input and directly insert it into the page's Document Object Model (DOM).
      
    - **Stored Input**: The application might retrieve previously submitted and stored input (e.g., a user comment from a database) and display it without proper sanitization.

- **Potential Impacts**:
	- **Phishing**: Attackers can inject malicious forms (e.g., a fake login panel) to steal user credentials.
	  
	- **Web Page Defacement**: Attackers can alter the appearance of a web page, insert unauthorized advertisements, or completely replace its content, leading to significant reputational damage.


## References:

