
2025-07-29 15:26

Tags: #web  

## POST

- **Purpose**: Web applications use **POST** requests primarily when they need to *transfer files* or *move user parameters out of the URL and into the HTTP Request body.*

- **Fundamental Difference from GET**: Unlike **GET** requests where parameters are appended to the URL, **POST** requests place data within the **body of the HTTP request.**

#### POST vs GET

- **Lack of Logging**: Servers typically do not log the body of a request, making it more efficient and secure for transferring large or sensitive data like file uploads.
  
- **Fewer Encoding Requirements**: The request body can accept binary data directly, reducing the need for URL encoding that is necessary for data passed in a URL.
  
- **Larger Data Capacity**: POST requests are not constrained by URL length limits imposed by browsers and web servers (which are generally around 2,000 characters), allowing for the transmission of much larger amounts of data.


## Login Forms

- **Login Forms**: Credentials (e.g., `username=admin&password=admin`) are sent in the body of a POST request to authenticate a user.

![[Pasted image 20250730093702.png]]


## Authenticated Cookies

- **Authentication Cookies**: Upon successful login, the server responds with a `Set-Cookie` header (e.g., `PHPSESSID=...`). This cookie is used to *maintain the authenticated session for subsequent requests.* (check the **Storage tab** in Developer Tool)

- **Session Persistence**: A valid session cookie can be used to access authenticated parts of an application directly, *bypassing the login form*. This is a crucial concept in security, as stealing a valid cookie can lead to session hijacking.

- If you **LOG OUT**, your cookie will be *unavailable* until you log in again
	- But you can *try different cookie* which has already been authenticated and skip the log in page like usual

- **Invalid**:
	- ![[Pasted image 20250730095503.png]]

- **Valid**:
	- ![[Pasted image 20250730095512.png]]


## cURL for POST

- To send a **POST** request, use the `$ -X POST $` flag.

- To include **data** in the request body, use the `$ -d $` flag (e.g., `$ -d 'username=admin&password=admin' $`).

- Example: `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i`

- To use a **cookie** for an authenticated request, use the `$ -b $` flag or the `$ -H 'Cookie: ...' $` header.
	- `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>`
	  
	- `curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`

## JSON data

- When an application endpoint expects JSON, the data must be formatted accordingly (e.g., `$ '{"search":"london"}' $`).

![[Pasted image 20250730100801.png]]

- The `$ Content-Type: application/json $` header **must be included** to inform the server of the data format.

## References:
https://academy.hackthebox.com/module/35/section/224