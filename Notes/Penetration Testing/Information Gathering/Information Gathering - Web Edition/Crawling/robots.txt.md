
2025-09-20 14:06

Tags: #web   

## robots.txt

- It is a simple **text file** located in the root directory of a website (e.g., `www.example.com/robots.txt`).
  
- It functions as a set of guidelines for web crawlers (bots), **specifying which areas of the website they are permitted to access and which are off-limits.**
  
- It adheres to the Robots Exclusion Standard, an unofficial standard for web etiquette.

![[Pasted image 20250920141149.png]]

#### How it Works

- The file contains "directives" that apply to specific **"user-agents"** (identifiers for different bots like Googlebot or Bingbot).
	- A **wildcard** character (`*`) can be used to apply rules to all user-agents.

- **Common directives include:**
	- `Disallow`: Instructs bots not to crawl a specific path (e.g., `Disallow: /admin/`).
	  
	- `Allow`: Explicitly permits bots to crawl a path, even if it's part of a broader disallowed directory.
	  
	- `Crawl-delay`: Sets a mandatory wait time (in seconds) between requests to avoid overloading the server.
	  
	- `Sitemap`: Provides a direct link to the website's XML sitemap for more efficient indexing.


## Importance in Web Reconnaissance

- For security professionals, `robots.txt` is a valuable intelligence source.

- **Discovering Hidden Directories:** The paths listed in `Disallow` directives often **point to sensitive areas** the website owner wants to hide from search engines, such as administrative panels, private files, or backup directories.

- **Mapping Website Structure:** Analyzing the **allowed and disallowed** paths helps create a basic map of the site's layout, potentially revealing unlinked pages or functionalities.

- **Detecting Security Measures:** The file might reveal *"honeypots"* or crawler traps, which are intentionally placed to lure malicious bots, providing insight into the target's defensive strategies.


## References:

https://academy.hackthebox.com/module/144/section/3077