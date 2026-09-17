
2025-07-25 10:56

Tags: #web  

## Development Frameworks & APIs

- **Purpose**: Frameworks *simplify* the creation of modern, complex web applications by providing *pre-built solutions* for common functionalities, such as user registration.

- **Necessity**: Building sophisticated web applications from scratch is challenging, making frameworks a common choice for development.

- **Examples**:
	- **Laravel (PHP)**: Used by startups and smaller companies.
	  
	- **Express (Node.JS)**: Used by PayPal, Uber, and IBM.
	  
	- **Django (Python)**: Used by Google, YouTube, and Instagram.
	  
	- **Rails (Ruby)**: Used by GitHub, Hulu, and Airbnb.

## APIs (Application Programming Interfaces)

- **Function**: APIs serve as *the bridge between the front end and back end*, facilitating data exchange and execution of tasks. The front end requests an action, and the back end processes it and returns a response.

- **Implementation**: Developers implement API functionality on the back end using **standards like SOAP or REST**.

- **API vs HTTP request:** The API defines _what you can ask for_, and the HTTP request is _how you actually ask for it_.

#### Query Parameters

- **Mechanism**: A method for sending specific arguments to a web page using `GET` and `POST` requests.
	- **`GET`**: Parameters are included directly *in the URL* (e.g., `/search.php?item=apples`).
		- Just paste the item you're looking for in the URL
		  
	- **`POST`**: Parameters are sent *within the body of the HTTP request*.

- **Use Case**: Allows a single page to process various types of input.

#### Web APIs

- **Definition**: An interface that specifies how a web application can *interact with other applications*, typically *over the HTTP protocol.*

- **Function**: Enables remote access to back-end functionality. For example, a weather app's API can retrieve weather data for a specific city.

#### SOAP (Simple Objects Access Protocol)

- **Data Format**: Uses **XML** for both requests and responses.

- **Strengths**:
	- Ideal for transferring highly structured, complex, or binary data.
	  
	- Effective for managing stateful interactions (e.g., maintaining the current state of a page).

- **Weakness**: Can be overly complex and verbose for simple queries.

#### REST (Representational State Transfer)

- **Data Format**: Typically returns data in **JSON** format, though other formats like XML are possible.

- **Mechanism**: Uses the URL path to define the resource being requested (e.g., `/users/1`).

- **Strengths**:
	- Promotes modular and scalable applications by breaking down functionality into smaller, distinct API calls.
	  
	- More efficient for simple queries like searching or filtering compared to SOAP.

- **HTTP Methods**: Utilizes different HTTP methods for specific actions (CRUD operations):
	- **`GET`**: Retrieve data.
	  
	- **`POST`**: Create new data.
	  
	- **`PUT`**: Create or replace existing data.
	  
	- **`DELETE`**: Remove data.
## References:

https://academy.hackthebox.com/module/75/section/762