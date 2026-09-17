
2025-02-25 15:01

Tags: #linux #bash  #hands-on

## Task Scheduling

- Task scheduling: automate tasks at specific time intervals

## Systemd

- Systemd is the service that used to start processes or scripts at specific time

- To set up:
	- Create a timer (schedules when your `mytimer.service` should run)
	- Create a service (executes the commands or script)
	- Activate the timer

- Create a timer:
	- Need to create a directory to store the timer
		- Ex: `sudo mkdir /etc/systemd/system/mytimer.timer.d`
	- In the timer file:
		- Unit: description for the timer
		- Timer: when to start
		- Install: where to install
		- ![[Pasted image 20250225150935.png]]

- Create a service
	- Set a description and specify the full path to the script we want to run
		- Ex: `sudo vim /etc/systemd/system/mytimer.service`
		- ![[Pasted image 20250225151500.png]]

- Activate the timer:
	- `sudo systemctl start mytimer.timer`
	- `sudo systemctl enable mytimer.timer`


## Cron

- Can also be used to schedule task at specific time

- Need to create ==contab== file

![[Pasted image 20250225151839.png]]

- The time is in order left -> right: minutes (0-59), hour (0-23), days of month (1-31), months (1-12), days of week (0-7)


## References:

