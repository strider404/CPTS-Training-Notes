
2025-02-28 15:17

Tags: #linux 

## File System

- Managing file system: ==organize, store, maintain data on disk==

- File systems in Linux:
	- ext2: old
	- ext3 & ext4: more advanced, has journaling (return from crash), ==ext4== is default for modern Linux systems (reliable, large file support)
	- Btrfs: has snapshot & integrity check
	- XFS: best at handling large files
	- NTFS: originally from Windows, used when dual-boot with Windows

- Linux's file architecture based on the Unix model, in a hierarchy structure

- ==Inodes== is the most important component. They're data structure that store metadata of files and directories, including permissions, ownership, size, and timestamps

- File's name is not stored, but the pointer to that file

- Inode table is the collection of inodes

- ==Inodes explain==: [Inode Structure](https://www.youtube.com/watch?v=tMVj22EWg6A&t=5s)

- Types of file in Linux:
	- Regular files
	- Directories: file that contain other files
	- Symbolic links: shortcut to files

## Disk & Drives

- Main tool for disk management: fdisk

- Fdisk can create, delete, manage partitions of the disk

- Each partitions can run a separated file system (Ex: 1 partition can run ext4, 1 can run ext3)

- Bash: `sudo fdisk -l`


## Mounting

- Mounting: ==link== a ==drive== or partition to a ==direction== in the file system hierarchy (must)

- After that, they can be used as regular directories

- Mount file in Linux: `mount`

- Mounted File systems at Boot: `cat /etc/fstab`

- List Mounted Drives: `mount`

- Mount a USB drive: `sudo mount /dev/sdb1 /mnt/usb`

- Unmount: `sudo umount /mnt/usb`


## Swap

- When RAM is full, the kernel use the Swap space in the disk instead

- `mkswap`: prepare devices or files for creating swap space

- `swapon`: activate swap space


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2096)