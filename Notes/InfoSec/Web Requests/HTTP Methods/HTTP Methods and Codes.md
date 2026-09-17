
2025-07-29 10:58

Tags: #web  

## HTTP Request Methods

- **HTTP methods instruct a web server on how to process a client's request for a resource**. The availability of these methods depends on server and application configurations.

| **Method** | **Description**                                                                                                                                             |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `GET`      | *Requests a specific resource*. Additional data can be passed to the server via query strings in the *URL* (e.g. `?param=value`).                           |
| `POST`     | *Sends data (e.g., from forms, files) to the server* in the request's *body*.                                                                               |
| `HEAD`     | *Requests only the headers* of a resource, without the body. This is useful for checking resource's length before a full `GET` request.                     |
| `PUT`      | *Creates* a new resource on the server.                                                                                                                     |
| `DELETE`   | *Deletes* an existing resource on the webserver. If not properly secured, can lead to Denial of Service (DoS) by deleting critical files on the web server. |
| `OPTIONS`  | *Returns information* about the server, such as the methods accepted by it.                                                                                 |
| `PATCH`    | *Applies partial modifications* to the resource at the specified location.                                                                                  |

- **Note**: While `GET` and `POST` are the most common, applications using REST APIs frequently utilize `PUT` and `DELETE` for data manipulation.

## HTTP Status Codes

- **HTTP status codes are responses from the server that indicate the outcome of a client's request**. They are categorized into five classes.

- [Full list](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)

- **`1xx` (Informational)**: The request was received and is being processed.


- **`2xx` (Successful)**: The request was successfully received, understood, and accepted.
	- **`200 OK`**: The request succeeded.


- **`3xx` (Redirection)**: Further action is needed to complete the request.
	- **`302 Found`**: The client is temporarily redirected to another URL.


- **`4xx` (Client Error)**: The request contains an error or cannot be fulfilled.
	- **`400 Bad Request`**: The server cannot process a malformed request.
	  
	- **`403 Forbidden`**: The client lacks the necessary permissions for the resource.
	  
	- **`404 Not Found`**: The requested resource does not exist on the server.


- **`5xx` (Server Error)**: The server failed to fulfill a seemingly valid request.
	- **`500 Internal Server Error`**: An unexpected condition on the server prevented it from fulfilling the request.
## References:

https://academy.hackthebox.com/module/35/section/221