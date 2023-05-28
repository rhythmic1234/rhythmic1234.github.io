---
layout: post
title:  "Obsidian vault sync from iCloud to Google Drive"
---

In this post, I will describe a way to do (one-way) sync of your Obsidian vault from iCloud to Google Drive.

# The problem
I use Obsidian in my iPad + mac.

But I want to be able to use my vault from my android phone too.

But trying to do two way sync by pointing to same folder is making both iCloud and gDrive unstable.

# Existing solutions
Obsidian Sync and other sync solutions (like MultCloud, syncToy, FolderSync) are too expensive.

# Aim
From my phone, I want to **at least view** my notes  (giving up editing).

So, my aim has became to do one-way sync from iCloud to Google Drive.
I will do this using my old Macbook, keeping it open and running a cron job.

# Solution
My solution steps are to...
1. Find out location of iCloud and Google Drive, since we need to access from terminal
2. Ensure that `crontab` and `rsync` binaries can access iCloud + Google drive folders from MacOS terminal
3. Prepare the script using `rsync`
4. Setup a cronjob to run our script every hour
5. Prevent Mac from sleeping to run cronjobs properly

## 1- Find out source and destination folder
Find out source folder in iCloud. In `~/Library/Mobile\ Documents/` folder find the folder you want to sync from iCloud.

In my case, Obsidian data is in `iCloud~md~obsidian/Documents/Obsidian`

Create destination folder (in Google Drive). The relative path can be like `~/Google\ Drive/My\ Drive/Obsidian/`

## 2- Giving full disk access to crontab and rsync binaries
This is required due to Apple's privacy and security policies.

a. Go to System Preferences/Security & Privacy/Privacy. Click + to add an app.

b. Click "Cmd + Shift + g" to pick custom path (both _crontab_ and _rsync_ is in **/usr/bin/**)


## 3- Sync script
### Install latest rsync via brew
Default rsync shipped in MacOS may give following [error](https://www.jafdip.com/how-to-fix-rsync-error-code-23-on-mac-os-x/):

`rsync error: some files could not be transferred (code 23) at ...`

So install latest rsync via brew.

Then find the binary location, which should be: `/usr/local/opt/rsync/bin/rsync`

(*/usr/local/opt is a symbolic link used by brew*)

### obsidian-sync.sh
So our script should look like as follows:
```bash
#!/bin/zsh

OBSIDIAN_SOURCE=~/Library/Mobile\ Documents/iCloud~md~obsidian/Documents/Obsidian/
OBSIDIAN_DEST=~/Google\ Drive/My\ Drive/Obsidian/

# Print date (for logging)
echo "==== ===== ===="
echo $(date)

# synchronize files from iCloud directory to Google Drive directory
rsync -ahv --delete $OBSIDIAN_SOURCE $OBSIDIAN_DEST

# force iCloud to re-sync
killall bird
```

Don't forget to give execute permission to the file `chmod +x obsidian-sync.sh`

## 4- Setting cron job
```bash
# open via `crontab -e` and type the config below
0 * * * * ~/obsidian-sync.sh > ~/obsidian-sync.log 2>&1
```

## 5- Prevent Mac from sleeping
This is optional. Since I don't use my old mac, I make sure it is awake continuosly.

# Conclusion

I have described a simple way to sync files from iCloud to Google Drive. I needed this for accessing my Obsidian vault in iCloud, but you can use it for any other folders you want to sync.

Enjoy.
