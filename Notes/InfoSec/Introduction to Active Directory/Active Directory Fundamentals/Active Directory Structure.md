
2025-07-04 15:23

Tags: #ad  

## Active Directory Structure

- **Data Accessibility**: AD is fundamentally a database accessible to all domain users. A standard user account can enumerate a significant amount of information, including:
	- Domain Computers and Users
	  
	- Group Information and Organizational Units (OUs)
	  
	- Domain Policies (Default, Functional Levels, Password)
	  
	- Group Policy Objects (GPOs)
	  
	- Domain Trusts
	  
	- Access Control Lists (ACLs)

## Hierarchical Structure

- **Tree-like structure**:
	- **Forest**: The *highest-level container* and the ultimate security boundary. All objects within a forest are under a common administrative control. A forest can contain one or more domains.
	  
	- **Domain**: A *core unit* of logical organization within a forest. It contains objects like users, computers, and groups. Domains can have child domains.
		- The first domain created in a forest is called the **forest root domain**.
		  
	- **Child Domain**: A *domain created directly under another domain* (its parent). It shares a contiguous namespace with its parent (e.g., `corp.inlanefreight.local` is a child of `inlanefreight.local`).
	  
	- **Organizational Unit (OU)**: A *container within a domain* used to *organize objects like users, groups, and computers*. OUs allow for the delegation of administrative control and the **application of specific Group Policies.**
		- Can contain **sub-OUs**

- *Example*:
INLANEFREIGHT.LOCAL *//forest root domain*
├── ADMIN.INLANEFREIGHT.LOCAL *//child domain*
│   ├── GPOs *//Group Policies*
│   └── OU *//OUs*
│       └── EMPLOYEES *//sub-OUs*
│           ├── COMPUTERS
│           │   └── FILE01
│           ├── GROUPS *// Group*
│           │   └── HQ Staff
│           └── USERS 
│               └── barbara.jones *// User*
├── CORP.INLANEFREIGHT.LOCAL *//child domain*
└── DEV.INLANEFREIGHT.LOCAL *//child domain*

![[Pasted image 20250704160221.png]]


#### Domain Trusts

- **Purpose**: Trusts are established to *allow users in one domain to access resources in another*. This is a common practice in organizations that have undergone mergers or acquisitions.

![[Pasted image 20250704160358.png]]

- Users in `INLANEFREIGHT.LOCAL` can access resources in `FREIGHTLOGISTICS.LOCAL` and vice versa.

- But in the other domains (`CORP.INLANEFREIGHT.LOCAL`; `DEV.INLANEFREIGHT.LOCAL`;...) *cannot* because they don't have trust 


## References:

[Introduction to Active Directory](https://academy.hackthebox.com/module/74/section/700)