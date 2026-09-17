
2025-09-22 09:24

Tags: #web  

## Creepy Crawlies

- **Web crawling tools** automate the *process of navigating and extracting data* from websites, making reconnaissance faster and more efficient.


#### Popular Web Crawlers

- **Burp Suite Spider:** An active crawler within Burp Suite, effective for mapping web applications and identifying hidden content.

- **OWASP ZAP (Zed Attack Proxy):** A free, open-source security scanner with a spider component to crawl sites and find vulnerabilities.

- **Scrapy:** A scalable and versatile Python framework used to *build custom web crawlers* for extracting structured data.

- **Apache Nutch:** A powerful, open-source Java crawler designed for large-scale crawling projects, though it requires more technical setup.


## ReconSpider: A Custom Scrapy Tool

- **Purpose:** `ReconSpider` is a *custom web spider built* using the **Scrapy framework**, designed specifically for reconnaissance tasks.

- **Installing**:
![[Pasted image 20250922093025.png]]


- **Output:**
![[Pasted image 20250922093055.png]]


- The crawled data is saved in a JSON file named `results.json`.

- This file contains structured information categorized by keys, providing insights into the **website's architecture and content**. The key categories include:
	- `emails`: Discovered email addresses.
	  
	- `links`: Internal and external URLs found on the site.
	  
	- `external_files`: Links to external files like PDFs.
	  
	- `js_files`: URLs of JavaScript files.
	  
	- `form_fields`: Information about forms on the website.
	  
	- `images`, `videos`, `audio`: URLs to multimedia content.
	  
	- `comments`: HTML comments found in the source code.
## References:
https://academy.hackthebox.com/module/144/section/3079
