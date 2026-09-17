
2025-09-20 13:45

Tags: #web  

## Crawling

- **Definition:** Crawling, or spidering, is an automated process where *bots, known as web crawlers, systematically browse the internet by following links from one page to another to discover and index content.*

- **Mechanism:**
	- The process begins with an initial "seed URL."
	  ![[Pasted image 20250920134824.png]]
	- The crawler fetches the page, parses its content, and extracts all hyperlinks.
	- ![[Pasted image 20250920134839.png]]
	  
	- These discovered links are added to a queue to be crawled, and the process repeats iteratively.



#### Breadth-First Crawling

![[Pasted image 20250920134951.png]]

- **Explores all links on a given level of a website before moving to the next level deeper.** It is effective for obtaining a broad overview of a site's structure.


#### Depth-First Crawling

![[Pasted image 20250920135034.png]]

- **Follows a single link path as deeply as possible before backtracking to explore other paths.** It is useful for locating specific content deep within a website.


## Information Extraction and Analysis

- **Valuable Data:** Crawlers can extract various types of information crucial for reconnaissance:
	- **Links:** Both internal and external links help in mapping a website's structure and its connections to other resources.
	  
	- **Comments:** User comments can inadvertently expose sensitive information or operational details.
	  
	- **Metadata:** Information like page titles, keywords, and author details provides context about the content.
	  
	- **Sensitive Files:** Crawlers can be configured to find exposed **backup files** (`.bak`), **configuration files** (`web.config`), or log files that may contain confidential data like credentials or API keys.


## References:

https://academy.hackthebox.com/module/144/section/3076