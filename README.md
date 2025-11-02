# nottingham-cs-notes
All my notes for the University of Nottingham’s Computer Science (with Artificial Intelligence) BSc honours programme. Files are automatically updated and deployed at midnight UK time every day. Visible on [notes.oling.dev](https://notes.oling.dev) and on [GitHub](https://github.com/Draggie306/nottingham-cs-notes).

These notes are intended as a "spiritual successor" to my [Cheat Sheets on iBaguette](https://ibaguette.com/cheatsheets); they are nowhere near as polished, but should remain useful to an extent.

## View notes

### [Year 2 - All Notes](/Year%202/)
- [Semester 1 modules](/Year%202/Semester%201), including:
	- COMP2007 - Operating Systems and Concurrency
	- COMP2013 - Developing Maintainable Software
	- COMP2065 - Introduction to Formal Reasoning
- Semester 2 modules, coming soon.
- All-year modules, including:
	-  COMP2002 - Software Engineering Group Project


### [Year 1 - All Notes](/Year%201)
- [Semester 2 modules](/Year%201/Semester%202), including:
	- COMP1003 - Introduction to Software Engineering (theory)
	- COMP1004 - Databases and Interfaces (SQL, HTML, CSS and JS)
	- COMP1008 - Fundamentals of Artificial Intelligence (theory)
	- COMP1009 - Programming Paradigms (theory, Java and Haskell)
	- COMP1043 - Mathematics for Computer Scientists 2 (Linear Algebra)
- [Semester 1 modules](/Year%201/Semester%201), including:
	- COMP1001 - Mathematics for Computer Scientists 1 (Discrete Mathematics)
	- COMP1005 - Programming and Algorithms (ANSI C)
	- COMP1054 - Assembly Language Programming (theory & ARM32 assembly)
	- COMP1055 - Networks (theory & C implementations)
	- COMP1056 - Computer Architecture (theory, Hardware Description Language)

### Miscellaneous notes

- [University of Nottingham - GEOG1037 - Planet Earth: Exploring the Physical Environment](/Year%201/Semester%202/GEOG1037/Environmental%20Change) - 1 lecture note

## Setup & Automation
Every night at midnight, a cron job (see below) on my homelab syncs a S3-compatible storage bucket that contains my notes in Obsidian (which uses Remotely Save to sync notes to the bucket every 5 minutes) to this Git repo, and pushes them. Then, a Jekyll build is started on GitHub which renders and deploys the new, updated notes to the GitHub Pages site, visible on this page. 

> If the homelab is off (which should be never) then this repository will not be updated; usually, this should only be the case for a few days at most.

> Sometimes I write notes in a hurry and this (especially for mathematics) causes the Jekyll build to fail. I am notified when this happens and notes are usually fixed for the next day; if this persists, feel free to open a PR. It should be an easy fix.


## Maintenance
If the remote repository is pushed to, a manual push and sync is required to avoid conflicts before the cron job can run again successfully.


### Crontab expression
```sh
0 0 * * * cd /mnt/mega/uni-notes-git/ && /usr/bin/rclone sync --exclude .git/ --exclude .github/ r2:notes . -v && /usr/bin/git add . && /usr/bin/git commit -m "[cron] auto commit: update notes" && /usr/bin/git push &>> /mnt/mega/notes_sync.log
```

where `/mnt/mega` refers to the mount point of the external drive mounted in `/etc/fstab` as `UUID=<uuid> /mnt/mega ext4 nofail,defaults 0 2`, and `notes` is the name of the storage bucket. 

> Must exclude `.git` to reduce remote bucket Class A/B writes and storage used, and to speed up syncing.
> Must also exclude `.github` to not overwrite/remove Jekyll build settings.