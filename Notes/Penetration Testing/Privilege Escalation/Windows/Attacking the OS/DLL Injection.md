
2026-05-25 10:28

Tags: #escalation 

## DLL Injection

- **DLL Injection** is a technique where an attacker (or developer) *inserts a Dynamic Link Library (DLL) into a running process.* This forces the target process to execute the DLL's code within its own security context, allowing access to its resources or altering its behavior.


- **Legitimate Use:** Hot patching (e.g., Azure updating server code without forcing a reboot or downtime).


- **Malicious Use:** Evading security software by running malicious code inside a highly trusted, legitimate process (like `explorer.exe` or `svchost.exe`).

## The LoadLibrary Method

- This is the **classic** and most common injection technique. It utilizes the native Windows API to trick the target process into loading the malicious DLL.


- **The Injection Process (C code):**
	- **Target Acquisition:** Open a handle to the target process using `OpenProcess` with appropriate permissions (`PROCESS_ALL_ACCESS`).
	    
	- **Memory Allocation:** Allocate space _inside_ the target process's memory space for the path of the malicious DLL using `VirtualAllocEx`.
	    
	- **Writing the Path:** Write the actual file path string into that newly allocated memory using `WriteProcessMemory`.
	    
	- **Finding the API:** Get the memory address of the `LoadLibraryA` function from `kernel32.dll` (using `GetProcAddress`). Because `kernel32.dll` maps to the same address across processes, this address is valid in the target process.
	    
	- **Execution:** Call `CreateRemoteThread`, pointing its execution start to `LoadLibraryA` and passing the allocated DLL path as the argument. The target process is forced to spin up a thread and load your DLL.

## Manual Mapping

- An advanced, stealthy injection method designed to bypass anti-cheat and Endpoint Detection and Response (EDR) systems that actively monitor `LoadLibrary` calls.


- Instead of letting Windows handle the loading, the injecting tool acts as its own program loader.


- **Process:** It loads the DLL as raw data, manually maps the DLL sections into the target process's memory, manually resolves imports and relocations, executes Thread Local Storage (TLS) callbacks, and directly triggers `DllMain`.

## Reflective DLL Injection

- Created by Stephen Fewer, this technique injects a library from raw memory into a host process without relying on the OS loader. The library itself handles its own loading via an exported function, typically called `ReflectiveLoader`.


- **How it works step-by-step:**
	1. The raw DLL image is written into an arbitrary memory location within the host process.
	    
	2. Control is passed to `ReflectiveLoader` via `CreateRemoteThread()` or a bootstrap shellcode.
	    
	3. The `ReflectiveLoader` calculates its current location in memory and parses its own headers.
	    
	4. It locates `kernel32.dll` in the host process to find the addresses of `LoadLibraryA`, `GetProcAddress`, and `VirtualAlloc`.
	    
	5. It allocates a new, continuous memory region and maps its own headers and sections properly.
	    
	6. It processes its own import and relocation tables to fix memory references.
	    
	7. Finally, it calls its own `DllMain` with `DLL_PROCESS_ATTACH` to fully execute, returning control back to the initial thread when finished.

## DLL Hijacking

- **DLL Hijacking** takes advantage of the vulnerable way Windows applications search for and load external libraries during runtime. If an application attempts to load a DLL without specifying its absolute folder path, an attacker can place a malicious DLL in a directory searched _before_ the legitimate one.

## Safe DLL Search Mode

- Windows utilizes a specific search order when a program looks for a DLL. This sequence changes heavily depending on whether **Safe DLL Search Mode** is enabled or disabled in the registry (`HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\SafeDllSearchMode`).

|**Search Priority**|**Safe DLL Search Mode Enabled (Default)**|**Safe DLL Search Mode Disabled**|
|---|---|---|
|**1**|Directory from which the application loaded|Directory from which the application loaded|
|**2**|System Directory (`System32`)|**Current Directory**|
|**3**|16-bit System Directory|System Directory (`System32`)|
|**4**|Windows Directory|16-bit System Directory|
|**5**|**Current Directory**|Windows Directory|
|**6**|Directories listed in the `PATH` environment variable|Directories listed in the `PATH` environment variable|

## Execution Techniques

- To find potential hijacking opportunities, pentesters use tools like **Process Explorer** or **PE Explorer** to see what libraries an executable imports, or **Process Monitor (procmon)** filtered to the target application to watch real-time file system requests.


- There are two primary ways to weaponize this:

- **DLL Proxying**
	- If a program relies on a legitimate function (like an `Add` function) inside a critical DLL (`library.dll`), you can intercept it without crashing the application.
	  
	1. Rename the original DLL to something like `library.o.dll`.
	    
	2. Drop a malicious DLL named `library.dll` into the search path.
	    
	3. When the application calls `Add`, your malicious DLL intercepts the execution, handles your payload (e.g., tampering with data or spawning a shell), and then passes the execution seamlessly to the original `library.o.dll`. The application never realizes it was tricked.


- **Exploiting Invalid Libraries**
	- Sometimes applications aggressively check for optional or missing dependencies. By monitoring `procmon` for a status of `NAME NOT FOUND` ending in `.dll`, you can find paths where the executable looks for a library but fails to find it (e.g., looking for `x.dll` in the application folder).|
	  
	- **The Attack:** Drop a custom DLL named `x.dll` into that exact directory.
	    
	- **The Payload:** Put your execution code directly inside the `DLL_PROCESS_ATTACH` case of the `DllMain` entry point function. The moment the application attempts to check for that missing file, it automatically loads your library and triggers your code.
## References:

https://academy.hackthebox.com/app/module/67/section/2501