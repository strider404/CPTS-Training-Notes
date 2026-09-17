
2025-07-21 15:12

Tags: #web  

## Front End vs. Back End

- **Front-End:** Refers to the *client-side* of a web application; it is everything the user directly sees and interacts with in their browser.

- **Back-End:** Refers to the *server-side* of a web application; it drives the core logic, data processing, and functionalities that happen behind the scenes.

- **Full-Stack:** Encompasses both front-end and back-end development.


## Front-End Development

- **Core Technologies:**
	- **HTML (HyperText Markup Language)** for structure and content.
	  
	- **CSS (Cascading Style Sheets**) for design, layout, and animations.
	  
	- **JavaScript** for interactivity and functionality.

- **Key Responsibilities:**
	- Designing the visual concept, User Interface (UI), and User Experience (UX).
	  
	- Ensuring the application is responsive and functions correctly across all browsers, devices, and screen sizes.

- **Performance Considerations:**
	- Poorly optimized front-end code *can make an entire application feel slow* and unresponsive, even if the back-end server is fast. The issue resides on the client-side.

## Back-End Development

- **Core Components:**
	- **Back-end Servers:** The hardware and operating system (e.g., Linux, Windows) that host the application.
	  
	- **Web Servers:** Software that handles *HTTP requests* (e.g., Apache, NGINX, IIS).
	  
	- **Databases:** Systems for storing and retrieving application data (e.g., MySQL, PostgreSQL, MongoDB).
	  
	- **Development Frameworks:** Structures for building the core application logic (e.g., Django, Laravel, ASP.NET).


- **Key Responsibilities:**
	- Developing the *primary logic* and services.
	  
	- Managing the *database*.
	  
	- Creating *APIs* for communication with the front-end.
	  
	- Integrating *third-party services* and cloud infrastructure.

## Securing Front/Back End

- **Testing Methodologies:**
	- **Whitebox Pentesting:** Analyzing components with *full access* to the source code, typically feasible for the front-end.
	  
	- **Blackbox Pentesting:** Testing components *without access* to the source code, which is the *default approach* for the back-end.

- **Vulnerability Landscape:**
	- Both front-end and back-end have unique vulnerabilities. The **back-end** is particularly susceptible to *injection attacks* (e.g., SQL Injection, Command Injection) that manipulate how the server processes data.
	  
	- Vulnerabilities like Local File Inclusion (LFI) can potentially *expose back-end source* code, allowing for a more in-depth (whitebox) analysis.

## References:

https://academy.hackthebox.com/module/75/section/752