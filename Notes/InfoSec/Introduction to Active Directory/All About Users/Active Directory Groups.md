
2025-07-11 11:41

Tags: #ad  

## Active Directory Groups

- **Groups** in Active Directory (AD) are used to *collect similar users, computers, and other objects* to simplify the *mass assignment* of rights, permissions, and access to resources like printers and file shares.

- **Groups vs. Organizational Units (OUs):**
	- **Groups:** Primarily used to *assign permissions* to resources.
	    
	- **OUs:** Used to organize objects (users, groups, computers) for easier management and to *apply Group Policy settings*. OUs can also be used to delegate administrative tasks without granting broader administrative rights.

![[Pasted image 20250711114927.png]]

#### Group Types

- **Security Groups:** Used to *assign permissions and rights* to resources. Members inherit the permissions assigned to the group.
  
- **Distribution Groups:** Used by *email applications* (e.g., Microsoft Exchange) as mailing lists. They cannot be used to assign permissions.

#### Group Scope

- **Domain Local:** Can only be used to manage permissions for resources *within the same domain it was created* in. However, it can **contain members (users, global groups, universal groups) from any domain in the forest** and other domain local groups from its own domain.

- **Global:** Can be used to grant access to resources in *any trusted domain*. It can **only contain accounts from the domain where it was created**. Global groups can be members of other global groups (from the same domain), domain local groups, and universal groups.

- **Universal:** Can be used to manage resources across *multiple domains within the same forest*. They can contain **members from any domain**. Changes to universal group membership trigger forest-wide replication, which can increase network overhead.


#### Built-in vs. Custom Groups

- AD includes several built-in groups with **predefined** administrative roles (e.g., Domain Admins, Administrators). Organizations also create **custom** groups for specific needs.

#### Nested Group Membership

- **A group can be a member of another group.** This can lead to a user *inheriting* privileges indirectly, which can be difficult to track and may create unintended access paths. Tools like **BloodHound** are used to identify these complex privilege escalations.

#### Attributes

- `cn`: The `cn` or Common-Name is the name of the group in Active Directory Domain Services.
  
- `member`: Which user, group, and contact objects are members of the group.
  
- `groupType`: An integer that specifies the group type and scope.
  
- `memberOf`: A listing of any groups that contain the group as a member (nested group membership).
  
- `objectSid`: This is the security identifier or SID of the group, which is the unique value used to identify the group as a security principal.

## References:
https://academy.hackthebox.com/module/74/section/702
