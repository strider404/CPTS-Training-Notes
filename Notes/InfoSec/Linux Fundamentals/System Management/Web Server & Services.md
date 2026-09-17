
2025-02-27 12:34

Tags: #linux #bash #web #network  

## Start the server

- Most used [web server](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FNetwork%20Services) is Apache 

- The port can be configured in  `/etc/apache2/ports.conf`

 - Command: 
	 - `sudo systemctl start apache2` : start a web server on port 80


## CURL

- cURL: used to ==transfer file== over the shell by protocols like `HTTP`, `HTTPS`, `FTP`, `SFTP`, `FTPS`, or `SCP`, can control the web over the CLI

- Basically, return the web's source code to STDOUT

- Ex: `curl http://localhost`

## WGET

- wget: download files or web's content from FTP or HTTP to our local computer

- Ex: `wget http://localhost`

- curl vs wget: one return to STDOUT, one download & store locally

## PYTHON3

- Can also be used to start a web server (default port 8000)

- Ex: `python3 -m http.server`


## NPM & PHP

- Can also host a web server with npm & php

- npm is a package manager (like apt); install the http-server package & use options to specific port

- php can host through the -S option

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/74)