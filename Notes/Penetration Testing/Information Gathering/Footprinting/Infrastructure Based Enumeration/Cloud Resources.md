
2025-09-03 15:40

Tags: #footprint 

## Cloud Resources

- **Common Vulnerability**: A frequent issue is storage services—such as AWS S3 buckets, Azure blobs, or GCP cloud storage—being **configured to allow unauthenticated access.**


- **Discovery Methods**: Several techniques can be used to find these exposed cloud resources:
	- **DNS Enumeration**: Attackers can analyze a company's DNS records to find subdomains pointing to cloud storage services (e.g., `s3-website-us-west-2.amazonaws.com`).
		- ![[Pasted image 20250903154739.png]]
		  
	- **Google Dorking**: Using specific Google search operators like `inurl:` and `intext:` combined with a company's name can reveal publicly indexed files stored in the cloud.
		- ![[Pasted image 20250903154952.png]]
		  
	- **Source Code Analysis**: Inspecting the source code of a company's website can reveal links to assets (images, JavaScript, CSS) hosted on external cloud storage.
		- ![[Pasted image 20250903155312.png]]
		  
	- **Third-Party Tools**:
		- Services like **domain.glass** can provide insights into a company's infrastructure and DNS setup.
			- ![[Pasted image 20250903155509.png]]
			  
		- Platforms like **GrayHatWarfare** are specialized search engines for finding open cloud storage buckets and the files they contain across AWS, Azure, and GCP.
			- ![[Pasted image 20250903155522.png]]


## References:

https://academy.hackthebox.com/module/112/section/1062