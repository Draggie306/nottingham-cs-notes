# nottingham-cs-notes
All my notes for the University of Nottingham’s Computer Science (with Artificial Intelligence) BSc honours programme. Files are automatically updated at midnight UK time every day.

These notes are intended as a "spiritual successor" to my Cheat Sheets on iBaguette; they are nowhere near as polished, but should remain useful to an extent.

## Setup & Automation
Every night at midnight, a cron job on my homelab syncs a S3-compatible storage bucket that contains my notes in Obsidian (powered by Remotely Save) to this Git repo, and pushes them. Then, a Jekyll build is started on GitHub which deploys the new and updated notes to the GitHub Pages site, visible on this page. 

> If the homelab is off (which should be never) then this repository will not be updated; usually, this should only be the case for a few days at most.

> Sometimes I write notes in a hurry and this (especially for mathematics notes) causes the Jekyll build to fail. I am notified when this happens and notes are usually fixed for the next day; if this persists, feel free to open a PR. It should be an easy fix.


## Maintenance
If the remote repository is pushed to, a manual push and sync is required to avoid conflicts before the cron job can run again successfully.
