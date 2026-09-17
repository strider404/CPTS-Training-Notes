
2025-02-28 13:47

Tags: #linux  

## Backup & Restore

- Popular tools for backing up:
	- Rsync: open-source, only backup what is changed
	- Duplicity: Rsync but data is encrypted
	- Deja Dup: has graphic interface, uses Rsync, also encrypted

- Compression vs Incremental backup:
	- Compression: Reduce data size by remove rebundancy
	- Incremental: only backup what has changed from last time


## Rsync

- Backup a local Directory to our Backup-Server
	- `rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory`
	- copy the entire directory (`/path/to/mydirectory`) to a remote host (`backup_server`), to the directory `/path/to/backup/directory`
	- `archive` (`-a`): preserve the original file attributes, such as permissions, timestamps, etc
	- `verbose` (`-v`): provides a detailed output of the progress of the `rsync` operation


- Compression and incremental backups:
	- `rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory`
	- -z: compression
	- --backup: creates incremental backups in /path/to/backup/folder
	- --delete: removes files from the remote host that is no longer present in the source directory

- Restore backup:
	- `rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory`

- Encrypted Rsync:
	- `rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory`
	- Combine with SSH for encryption

- Auto-Synchronization:
	- Use combination of [cron](obsidian://open?vault=Pentester&file=01%20-%20Notes%2FInfoSec%2FLinux%20fundamentals%2FTask%20Scheduling) & rsync
	- Because we use ssh, so need to bypass the key authentication
	- Generate a key pair: `ssh-keygen -t rsa -b 2048`
	- Then provide the passphrase at ~/.ssh/id_rsa
	- Copy public key to remote server: `ssh-copy-id user@backup_server`
	- Create a script to trigger rsync (RSYNC_Backup.sh): `rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory`
	- Grant permission to the right user: `chmod +x RSYNC_Backup.sh`
	- Create a crontab: `cronjob -e`
	- Then adjust the timing


## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/18/section/2095)
