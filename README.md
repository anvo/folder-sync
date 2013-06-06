# folder-sync

*folder-sync* is a little helper script to place a specific folder into tmpfs for a short amount of time.

*folder-sync* is inspired by profile-sync-daemon/anything-sync-daemon, but aims at a more temporary usage for varying folders.

**This is an early and rough version of the script. There are no safety checks included, yet. But for now, it does the job quite well.**

## Usage

	folder-sync [-h] [-v] [-t tmpfs] [target]

## Options
		-h              Display help
		-v              Be verbose
		-t tmpfs        Set tmpfs

## Requirements
 * realpath
 * rsync

## Workflow
*folder-sync* works in two steps. At first, it copies the content of the target folder to the tmpfs. Then it renames the folder and creates a symbolic link with the original name pointing to the folder in the tmpfs.

Now, *folder-sync* waits until the user has finished its work.

At last, *folder-sync* copies the content of the folder in the tmpfs back to the disk, replaces the symbolic link with the folder on disk, and deletes the folder in the tmpfs.

## Example

	anvo@thinkpad:~$ folder-sync -v myFiles/
	Syncing /home/anvo/myFiles to tmpfs.
	TMPFS = /run/shm
	FOLDER = /home/anvo/myFiles
	RAMDIR=/run/shm/folder-sync/home/anvo/myFiles
	BACKUPDIR=/home/anvo/myFiles-diramsync

	Press [ENTER] to sync back to disc.

	Syncing /home/anvo/myFiles back to disc.


## Related tools
 * [anything-sync-daemon](https://github.com/graysky2/anything-sync-daemon)
 * [profile-sync-daemon](https://github.com/graysky2/profile-sync-daemon)
 * [ramlog](http://www.tremende.com/ramlog/)
 * [vmtouch](https://github.com/hoytech/vmtouch)