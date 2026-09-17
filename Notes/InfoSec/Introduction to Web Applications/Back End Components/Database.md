
2025-07-25 10:37

Tags: #web  

## Database

- **Purpose**: Web applications use backend databases to **store application assets** (images, files), content (posts, updates), and user data (credentials).

- **Function**: They enable *dynamic content* tailored to individual users and allow for fast data storage and retrieval.

## Relational (SQL) Databases

- **Structure**: Data is organized into tables, rows, and columns.

- **Relationships**: Unique keys are used to link different tables, creating relationships. The overall structure of these relationships is called a **Schema**.

- **Use Case**: They are highly efficient and reliable for large datasets with a clear, predefined structure.

![[Pasted image 20250725104232.png]]

- **Common Examples**:
    - **MySQL**: A widely used, free, and open-source database.
      
    - **MSSQL**: Microsoft's relational database, common with Windows Servers.
      
    - **Oracle**: A powerful, though potentially costly, database for large enterprises.
      
    - **PostgreSQL**: A free, open-source, and highly extensible database.


## Non-relational (NoSQL) Databases

- **Structure**: They do not use a rigid structure of tables and columns. Data is stored using various models.

- **Characteristics**: Known for being highly scalable and flexible, making them ideal for datasets that are not well-defined or structured.

- **Storage Models**:
	- Key-Value
	  
	- Document-Based
	  
	- Wide-Column
	  
	- Graph

![[Pasted image 20250725104520.png]]

- **Example (JSON):**
	- 
	`{`
	`"100001": {`
	`"date": "01-01-2021",`
	`"content": "Welcome to this web application."`
	`},`
	`"100002": {`
	`"date": "02-01-2021",`
	`"content": "This is the first post on this web app."`
	`},`
	`"100003": {`
	`"date": "02-01-2021",`
	`"content": "Reminder: Tomorrow is the ..."`
	`}`
	`}`

- **Common Examples**:
	- **MongoDB**: A popular open-source, document-based database that uses JSON-like objects.
	  
	- **Elasticsearch**: An open-source database optimized for fast searching and analysis of large datasets.
	  
	- **Apache Cassandra**: A free, open-source, and highly scalable database designed for fault tolerance.

#### Use in Web Applications

- **Integration**: Modern development languages (e.g., PHP) and frameworks provide straightforward methods to connect and interact with databases.

- **Process**:
    1. The database is installed and configured on the backend server.
       
    2. The web application establishes a connection to the database.
       
    3. The application sends queries (e.g., using SQL syntax) to store or retrieve data.


## References:

https://academy.hackthebox.com/module/75/section/761