
2025-04-12 16:13

Tags: #windows #shell #hands-on 

## Managing Services

- Objective:
	- See what services are running
	- Disable antivirus
	- Modify services for escalation

## Service Controller

- `sc`: Windows command-line tool used to query, start, stop, and configure services both locally and remotely.
	- `sc query`: View status of services/drivers.
		- `sc query type= service`: view all services (notice the space)
		- `sc query windefend`: status of Windows Defender
	- `sc start <service>`: Start a service.
	- `sc stop <service>`: Stop a service.
	- `sc config <service> start= disabled`: Disable a service at startup
		- `start= auto`: enable again

- **Account permission**:
	- Standard user: cannot stop protected services (like windefend)
	- Administrator: still cannot stop system-protected services
	- ==SYSTEM==: full permission

- Sometimes we cannot stop a service because some other programs are depending on it

- Other tools:
	- `tasklist /svc`: Lists processes with associated services and PIDs.
	- `net start`: Lists all currently running services (`net stop`, `net pause`, `net continue`)
	- `wmic service list brief`: Provides a full table of all services (Name, PID, StartMode, State, etc.).


## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1612)
