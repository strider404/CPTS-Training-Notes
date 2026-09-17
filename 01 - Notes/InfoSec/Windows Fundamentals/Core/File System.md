
2025-03-10 15:44

Tags: #windows  

## File System

- Windows supports five file systems: FAT12, FAT16, FAT32, NTFS, and exFAT.
	- FAT12, FAT16 no longer used
	- FAT32 used in portable devices (USB)
	- *NTFS* used nowadays by default

- FAT32 vs NTFS:

| **Key Aspect**      | **FAT32**                                       | **NTFS**                                                                 |
| ------------------- | ----------------------------------------------- | ------------------------------------------------------------------------ |
| **Primary Use**     | ==Portable== storage (USBs, SD cards)           | Default for Windows internal storage                                     |
| **File Size Limit** | Maximum file size of ==4GB==                    | Supports very large files                                                |
| **Compatibility**   | ==Widely compatible== across various devices/OS | Limited support on mobile and older media devices                        |
| **Key Features**    | ==Lacks built-in security== and journaling      | Includes journaling, metadata support, and granular security permissions |

## Permission

| **Permission Type**      | **Key Points**                                                                                    |
| ------------------------ | ------------------------------------------------------------------------------------------------- |
| **Full Control**         | Grants complete control: read, write, modify, and delete files/folders.                           |
| **Modify**               | Allows reading, writing, and deletion of files/folders.                                           |
| **List Folder Contents** | Permits viewing and listing folder and subfolder contents; applied only to folders.               |
| **Read and Execute**     | Enables viewing, listing, and executing files and folders; applies to both files and folders.     |
| **Write**                | Permits adding new files to folders and modifying file contents.                                  |
| **Read**                 | Allows viewing file contents and listing folder/subfolder contents.                               |
| **Traverse Folder**      | Enables navigation through folder structures without granting full visibility of folder contents. |

- Permission can be ==inherit== from parent folders by default

## Integrity Control Access Control List (icacls)

- icacls: command-line tool to manage NTFS permissions

- List NTFS permissions:
![[Pasted image 20250310162230.png]]

- Inheritance settings:
	- `(CI)`: container inherit (permissions applied to subfolders of that folder)
	- `(OI)`: object inherit (permissions applied to files of that folder)
	- `(IO)`: inherit only (permissions does not applied to that folder but its files/subfolders)
	- `(NP)`: do not propagate inherit (no inheritance)
	- `(I)`: permission inherited from parent container

- Basic permissions:
	- `F` : full access
	- `D` :  delete access
	- `N` :  no access
	- `M` :  modify access
	- `RX` :  read and execute access
	- `R` :  read-only access
	- `W` :  write-only access

- Can be used to grant/remove user's permission (see in the cheatsheet)

## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/49/section/456)