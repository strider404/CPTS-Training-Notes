
2025-08-18 15:51

Tags: #nmap  

## Saving the Results

- **Purpose of Saving:** It is recommended to save Nmap scan results to compare the outcomes of different scanning methods later.

- **Available Output Formats:** Nmap provides three primary formats for saving scan results:
	- **Normal Output (`-oN`):** Saves results in a human-readable format with a `.nmap` extension, similar to what is displayed in the terminal.
	  
	- **Grepable Output (`-oG`):** Creates a `.gnmap` file formatted for easy parsing with command-line tools like `grep`.
	  
	- **XML Output (`-oX`):** Generates a `.xml` file, which is a structured format ideal for processing by other programs.

- **Saving in All Formats:** The `-oA <basename>` option can be used to save the scan results in all three formats simultaneously. Each file will be named using `<basename>` as a prefix (e.g., `target.nmap`, `target.gnmap`, `target.xml`).

- - **Creating Reports:**
    - The XML output is particularly useful for generating clear, professional reports.
      
    - A tool named `xsltproc` can be used to convert the `.xml` file into an easy-to-read `.html` file, which is suitable for documentation and presentation to non-technical individuals.
        - ![[Pasted image 20250818155222.png]]



## References:

https://academy.hackthebox.com/module/19/section/104