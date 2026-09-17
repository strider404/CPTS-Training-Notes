
2025-07-30 10:34

Tags: #web  

## API

- An **API (Application Programming Interface)** can be used to interact with a database.

- The URL in an API query typically specifies the resource, such as a **database table** and a **specific row** (e.g., `http://<SERVER_IP>:<PORT>/api.php/city/london`).
	- api.php: endpoint
	- city: table
	- london: row

- **CRUD** stands for the four fundamental operations performed on a database: **C**reate, **R**ead, **U**pdate, and **D**elete.


## CRUD Operations

- **Create**
    - **HTTP Method**: `$POST$`
      
    - **Description**: Adds a new entry to the database.
      
    - **Usage**: A `$POST$` request is sent to the API endpoint (e.g., `/api.php/city/`). The new data is included in the request body, typically in JSON format, and the `Content-Type: application/json` header must be set.
      
    - **Example**: `curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'`

- **Read**
	- **HTTP Method**: `$GET$`
	  
	- **Description**: Retrieves data from the database.
	  
	- **Usage**: A `$GET$` request is sent to the API endpoint. You can retrieve a specific entry (e.g., `/api.php/city/london`), search for partial matches (e.g., `/api.php/city/le`), or get all entries by leaving the search term blank (e.g., `/api.php/city/`).
	  
	- **Example**: `curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq`
		- `jq` to format the output based on JSON format


- **Update**
	- **HTTP Method**: `$PUT$` (or `$PATCH$`)
	  
	- **Description**: Modifies an existing entry in the database.
	  
	- **Usage**: A `$PUT$` request is sent to the URL of the specific entry to be modified (e.g., `/api.php/city/london`). The new data for the entry is sent in the request body. The text notes that `$PUT$` replaces the *entire entry,* while `$PATCH$` is used for *partial updates.*
	  
	- **Example**: `curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'`


- **Delete**
	- **HTTP Method**: `$DELETE$`
	  
	- **Description**: Removes a specified entry from the database.
	  
	- **Usage**: A `$DELETE$` request is sent to the URL of the specific entry to be removed (e.g., `/api.php/city/New_HTB_City`).
	  
	- **Example**: `curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City`



## References:
https://academy.hackthebox.com/module/35/section/227
