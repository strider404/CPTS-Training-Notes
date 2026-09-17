
2025-02-15 10:45

Tags: #linux  

## Linux Structure

- __Philosophy__

| __Principle__                                               | __Description__                                                                                      |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Everything is a file                                        | all configuration files are stored in 1 or more text files                                           |
| Small, single-purpose programs                              | various tools, each focus on single purpose, can combine to work together                            |
| Ability to chain programs together to perform complex tasks | integration and combination of tools to solve complex tasks                                          |
| Avoid captive user interfaces                               | mainly work with the shell (terminal)                                                                |
| Configuration data stored in a text file                    | An example of such a file is the `/etc/passwd` file, which stores all users registered on the system |

- __Components__

| __Component__   | __Description__                                                                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bootloader      | Code that run to start the system at the booting process (for Parrot it is GRUB)                                                                     |
| OS Kernel       | ==Manages resources== of I/O devices at hardware level                                                                                               |
| Daemons         | ==Background services==, to ensure some tasks like scheduling, printing,... work properly                                                            |
| OS Shell        | The ==interface== between user & the OS (use the CLI)                                                                                                |
| Graphics server | Provide a graphical sub-system (server) called "X" or "X-server" that allows graphical programs to run locally or remotely on the X-windowing system |
| Window Manager  | Graphical user interface (GUI)                                                                                                                       |
| Utilities       | Programs that perform particular functions for user or other programs                                                                                |

- **Architecture**

| **Layer**      | **Description**                                                                                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Hardware       | Physical devices (CPU,RAM,...)                                                                                                                               |
| Kernel         | ==Core== of Linux, it control hardware resources, allocates memory, access data,....Give each process its own resources to avoid conflicts between processes |
| Shell          | ==Command-line interface (CLI)==, for user to execute Kernel functions                                                                                       |
| System Utility | Make all the system functionalities available for users                                                                                                      |


- __File System Hierarchy__

| **Path** | **Description**                                                                                                                         |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `/`      | ==Root== filesystem, contains all files to boot the OS or other filesystems, all other filesystem mounted as ==subdirectories== of root |
| `/bin`   | essential command binaries                                                                                                              |
| `/boot`  | static bootloader, kernel executables, files required to boot the OS                                                                    |
| `/dev`   | device files, to access the hardware                                                                                                    |
| `/etc`   | local system/application configuration files                                                                                            |
| `/home`  | subdirectories for each users                                                                                                           |
| `/lib`   | library files for boot                                                                                                                  |
| `/media` | external removable media (USB)                                                                                                          |
| `/mnt`   | temporary mount point                                                                                                                   |
| `/opt`   | optional files                                                                                                                          |
| `/root`  | directory for root user                                                                                                                 |
| `/sbin`  | contain exe for system admin (binary system files)                                                                                      |
| `/tmp`   | temporary files of OS & programs                                                                                                        |
| `/usr`   | exe, lib,...                                                                                                                            |
| `/var`   | variable data files (log, email, cron files,...)                                                                                        |


## References:
[Linux Fundamentals](https://academy.hackthebox.com/module/18/section/94)
