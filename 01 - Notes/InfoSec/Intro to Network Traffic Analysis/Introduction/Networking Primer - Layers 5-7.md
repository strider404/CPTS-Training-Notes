
2025-06-25 10:04

Tags: #network  

## HTTP

- **Function**: A stateless Application Layer protocol for *transferring data*, such as *web pages*, between a client and a server.

- **OSI Layer**: *Application Layer - Layer 7* 

- **Transport**: Typically uses TCP over ports *80* or *8000*.

- **Security**: Transmits data in clear text, which is inherently *insecure*.

#### HTTP Methods

- `GET`: **Requests** and retrieves **data** from a specified resource. (*Required*)
  
- `HEAD`: **Requests the headers** of a resource, without the message body. Useful for server reconnaissance. (*Required*)
  
- `POST`: To **create** a new resource as a subordinate of the target URI. The **server is responsible for assigning the final URI** to the new resource.
  
- `PUT`: To **create or completely replace** a resource at a **specific URI known by the client.**
  
- `DELETE`: **Removes** the specified resource.
  
- `OPTIONS`: **Gathers information** on the HTTP methods that the server supports for a specific resource.
  
- `TRACE`: **Echos the received request** back to the client for diagnostic purposes.
  
- `CONNECT`: Reserved for use with **proxies** to establish a network **tunnel**.


## HTTPS

- **Function**: A *secure version of HTTP* that encrypts the communication channel.

- **Security**: Utilizes *Transport Layer Security (TLS) in Layer 6* or its predecessor, *Secure Sockets Layer (SSL)*, to *encrypt* the entire session. This protects against Man-in-the-Middle (MitM) attacks and eavesdropping.

- **Transport**: Uses TCP over ports *443* or *8443*.

- **Process**:
	- The client initiates a *TCP connection* to the server on a designated secure port (e.g., 443).
    
	- A **TLS Handshake** begins with a `ClientHello` message.
    
	- During the handshake, the client and server agree on cryptographic parameters, exchange digital certificates for authentication, and generate a shared secret key.
    
	- Once the handshake is complete, *all subsequent HTTP data is encrypted* and transmitted as TLS Application Data.

![[Pasted image 20250625104307.png]]


## FTP

- **Function**: An *Application Layer* protocol for *transferring files* between devices.

- **Security**: Considered *insecure* as it transmits commands and data, including authentication credentials, in clear text. Secure alternatives like SFTP are preferred.

- **Architecture**: Uniquely uses two separate TCP channels:
	- **Port 21**: The command/control channel for *session management.*
	  
	- **Port 20**: The data channel for the *actual file transfer.*

- **Operational Modes**:
	- **Active Mode (default)**: The *server initiates the data channel connection back to the client.* This can be problematic with firewalls and NAT.
	  
	- **Passive Mode**: The *client initiates the data channel connection to the server*, which is generally more compatible with modern network configurations.
		- 

#### FTP Commands

| **Command** | **Description**                                                    |
| ----------- | ------------------------------------------------------------------ |
| `USER`      | specifies the user to log in as.                                   |
| `PASS`      | sends the password for the user attempting to log in.              |
| `PORT`      | when in active mode, this will change the data port used.          |
| `PASV`      | switches the connection to the server from active mode to passive. |
| `LIST`      | displays a list of the files in the current directory.             |
| `CWD`       | will change the current working directory to one specified.        |
| `PWD`       | prints out the directory you are currently working in.             |
| `SIZE`      | will return the size of a file specified.                          |
| `RETR`      | retrieves the file from the FTP server.                            |
| `QUIT`      | ends the session.                                                  |

![[Pasted image 20250625104924.png]]


## SMB

- **Function**: A protocol used predominantly in *Windows* environments for *sharing resources* such as files, printers, and authenticated services.

- **Transport**: Has evolved over time and can operate over:
	- TCP port 445 (modern standard).
	- NetBIOS over TCP port 139.
	- NetBIOS over UDP ports 137 and 138.

- Connection-oriented (using TCP)

- Also performs *TCP handshake*:

![[Pasted image 20250625105222.png]]

## References:


[Practice using HTTP & FTP](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FNetwork%20Foundations%2FSkills%20Assessment)
