
2025-04-12 16:53

Tags: #windows #shell  #hands-on

## Working With Scheduled Tasks

- **Scheduled tasks**: used to ==automation==, but can also used for attackers to serve as ==persistence mechanism==

- Triggered by:
	- Time (daily, weekly, monthly)
	- System events (startup, user login, idle state)
	- Task registration or terminal session changes

- `schtask`: Work with scheduled task, display all scheduled task when used alone

- **Query existing tasks:** `schtasks /query`
	- e.g., `schtasks /query /v /fo list`

| **Action** | **Parameter** | **Description**                                                                                     |
| ---------- | ------------- | --------------------------------------------------------------------------------------------------- |
| Query      | (no flag)     | Performs a local or remote search for existing scheduled tasks. May be limited by user permissions. |
|            | `/fo`         | Sets output ==format==: `TABLE`, `LIST`, or `CSV`.                                                  |
|            | `/v`          | Enables ==verbose== output showing advanced task properties (used with `LIST` or `CSV`).            |
|            | `/nh`         | Omits column headers in `TABLE` or `CSV` output.                                                    |
|            | `/s`          | Specifies remote ==host== (`\\hostname`). Defaults to localhost.                                    |
|            | `/u`          | ==Username== for remote access (used with `/s`).                                                    |
|            | `/p`          | ==Password== for the user (used with `/u`).                                                         |


- **Create a New Task**: `schtasks /create`
	- e.g., `schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\path\ncat.exe 172.16.1.100 8100"`

| **Action** | **Parameter** | **Description**                                                      |
| ---------- | ------------- | -------------------------------------------------------------------- |
| Create     | (no flag)     | Schedules a new task on the local or remote system.                  |
|            | `/sc`         | Sets ==schedule== type: `MINUTE`, `HOURLY`, `DAILY`, `ONSTART`, etc. |
|            | `/tn`         | Sets the unique ==name== for the task.                               |
|            | `/tr`         | Defines the task's ==action== (program/script to execute).           |
|            | `/s`          | Specifies remote ==host== (optional).                                |
|            | `/u`          | ==Username== for authentication (optional, used with `/s`).          |
|            | `/p`          | ==Password== for authentication (optional, used with `/u`).          |
|            | `/mo`         | Modifier for ==schedule== (e.g., every 5 minutes).                   |
|            | `/rl`         | Run level: `LIMITED` (default) or `HIGHEST`.                         |
|            | `/z`          | Deletes the task automatically after completion.                     |

- **Modify an Existing Task**: `schtasks /change`
	- e.g., `schtasks /change /tn "TaskName" /ru username /rp password`

| **Action** | **Parameter** | **Description**                                          |
| ---------- | ------------- | -------------------------------------------------------- |
| Change     | (no flag)     | Modifies properties of an existing task.                 |
|            | `/tn`         | ==Identifies== the task to be modified.                  |
|            | `/tr`         | Modifies the ==command== or program run by the task.     |
|            | `/ru`         | Sets the user ==account== under which the task will run. |
|            | `/rp`         | Sets the ==password== for the user account.              |
|            | `/ENABLE`     | ==Enables== a previously disabled task.                  |
|            | `/DISABLE`    | ==Disables== an active task.                             |

- Delete a Scheduled Task: `schtasks /delete`
	- e.g., `schtasks /delete /tn "TaskName" /f`

| **Action** | **Parameter** | **Description**                                  |
| ---------- | ------------- | ------------------------------------------------ |
| Delete     | (no flag)     | Removes a task from the scheduler.               |
|            | `/tn`         | Specifies the ==task name== to delete.           |
|            | `/s`          | Targets a remote ==host== (optional).            |
|            | `/u`          | ==Username== for authentication (optional).      |
|            | `/p`          | ==Password== for authentication (optional).      |
|            | `/f`          | ==Forces deletion== without confirmation prompt. |

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/167/section/1613)
