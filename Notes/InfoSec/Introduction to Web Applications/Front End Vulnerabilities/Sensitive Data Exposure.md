
2025-07-23 10:06

Tags: #web  

## Front-End Security

- **Client-Side Nature**: Front-end components execute on the *client-side* (the user's browser).

- **Indirect Threat**: Vulnerabilities in these components *do not* typically pose a *direct threat to the back-end* infrastructure or cause permanent damage on their own.
  
- **User Risk**: The primary risk is to the **end-user**, who can be attacked if a front-end vulnerability is exploited.

#### Sensitive Data Exposure

- **Definition**: This vulnerability occurs when **sensitive information** is made available to the end-user in **clear-text**, most commonly within the client-side source code of a web application.

- **Location**: Such data can be found in the HTML, embedded or external JavaScript files, and code comments. This is **distinct** from the **back-end source code**, which should not be accessible from the client-side.

- *Reviewing the page source code is one of the first steps in a web application assessment* to find "low-hanging fruit."
  
- **Manual Inspection**:
    - Use the browser's "**View Page Source**" feature (often accessible via **right-click** or a keyboard shortcut like `Ctrl+U`).

- **Tooling**:
	- Web proxies such as Burp Suite can intercept and display the source code.
	  
	- Automated tools can scan source code to identify potential paths, directories, and other sensitive information.


## References:

https://academy.hackthebox.com/module/75/section/756