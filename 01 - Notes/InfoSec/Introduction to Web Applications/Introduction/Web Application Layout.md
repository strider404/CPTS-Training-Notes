
2025-07-21 10:40

Tags: #web  

## Web Application Layout

- **Definition**: A web application's layout encompasses its *infrastructure, components, and the architecture* that defines the relationships between them.

- **Uniqueness**: No two web applications are identical; they vary in purpose, design, programming, and back-end infrastructure.

- **Key Categories**: 
	- **Infrastructure**: The structure of *required* components, like servers and databases.
	  
	- **Components**: The *interactive parts* of the application, categorized as UI/UX, Client, and Server components.
	  
	- **Architecture**: The *relationships and interactions* between all components.


## Web Application Infrastructure

- **Client-Server**:
	- **Description**: This is the **fundamental mode**l for most web applications. A central **server** hosts the application's *back-end* logic and data, while the *front-end* components (UI) are sent to and executed on the **client's** web browser.
	  
	- **Interaction**: The client sends *HTTP requests* to the server (e.g., by clicking a button), and the server processes the request and sends a response back to be displayed by the client's browser.

![[Pasted image 20250721105433.png]]


- **One Server**:
	- **Description**: The *entire* application, including the database, is hosted on a single server.
	  
	- **Risk**: Extremely high risk. A compromise of one component or application can lead to the compromise of the entire server. It represents a single point of failure.

![[Pasted image 20250721105757.png]]


- **Many Servers - One Database**:
	- **Description**: The web application(s) and the database are hosted on separate servers.
	  
	- **Advantage**: Provides **segmentation**, which improves security. A compromise of a web server does not immediately grant access to the database server, and vice versa.

![[Pasted image 20250721112157.png]]


- **Many Servers - Many Databases**:
	- **Description**: Builds upon the previous model by further segmenting data. Each web application may have its own database, which can also be on a separate server.
	  
	- **Advantage**: This is one of the *most secure* and resilient models, offering strong access control and redundancy. It often requires tools like load balancers.

![[Pasted image 20250721112342.png]]


## Web Application Components

- **Client**
  
- **Server**
	- Webserver
	- Web Application Logic
	- Database

- **Services (Microservices)** 
	- 3rd Party Integrations
	- Web Application Integrations

- **Functions (Serverless)**


## Web Application Architecture

- **Three-Tier Architecture**: A common model for structuring application components.
	- **Presentation Layer**: The user interface (**UI**) that the client interacts with, typically consisting of HTML, CSS, and JavaScript.
	  
	- **Application Layer**: The "business logic" layer that *processes client requests*, handles authorization, and communicates with the data layer.
	  
	- **Data Layer**: Responsible for storing and retrieving data from the database.


- **Microservices**:
	- **Concept**: An architectural style where an application is built as a collection of *small, independent services*, each *focused on a single task* (e.g., payments, user authentication).
	  
	- **Benefits**: Promotes agility, flexible scaling, easy deployment, code reusability, and resilience. Services can be written in different programming languages.


- **Serverless**:
	- **Concept**: A *cloud computing model* where the cloud provider (e.g., AWS, Azure, GCP) manages the server infrastructure entirely.
	  
	- **Function**: Developers deploy code in stateless containers without needing to provision, scale, or maintain servers.


## References:

