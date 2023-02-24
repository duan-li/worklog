---
layout: post
title: Delete local Time Machine snapshots
date: 2021-09-14 11:36 +0000
---

## Time Machine

Time Machine is a backup and restore feature provided by Apple for macOS. It allows you to easily back up your entire Mac system, including files, applications, settings, and even the operating system itself. Time Machine makes it convenient to restore your system in case of data loss, accidental deletion, or hardware failures. 


In addition to backups, Time Machine also creates snapshots. Snapshots are point-in-time copies of your files and system state that are stored locally on your Mac. 

### Snapshots

Time Machine creates local snapshots on your Mac's internal storage when the backup disk is not available. These snapshots are temporary and can help you recover files even if the backup disk is disconnected.

Snapshots use the APFS file system's built-in snapshot functionality (available since macOS High Sierra). They capture the state of files and directories at a specific point in time without duplicating the entire data set. This approach ensures efficient use of disk space.

You can access and restore files from snapshots through the Time Machine interface or by using the "Enter Time Machine" option. This allows you to browse previous versions of files and recover specific items without performing a complete restore.

Snapshots are stored on your Mac's internal storage, which means they are subject to the available disk space. When the storage space is limited, older snapshots are automatically purged to make room for new ones.


### Summary

Both backups and snapshots provide data protection and recovery options in case of accidental file deletion, data corruption, or system issues. Time Machine's combination of periodic backups and local snapshots ensures that your data is safeguarded and easily recoverable, even in situations where the backup disk is unavailable.


## Delete local Time Machine snapshots

### tmutil command
The `tmutil` command in macOS is a command-line utility that allows you to interact with and manage various aspects of Time Machine, the built-in backup feature. It provides advanced functionality for controlling backups, managing backup disks, restoring files, and more. 


```bash

# list all local snapshots
tmutil listlocalsnapshots /

# delete snapshot by date
sudo tmutil deletelocalsnapshots 2020-10–09-002010

```

[How to fix “Not enough free space to install Big Sur” error](https://macpaw.com/how-to/not-enough-space-to-install-big-sur)


### Usage

```bash
Usage: tmutil version

Usage: tmutil enable

Usage: tmutil disable

Usage: tmutil startbackup [-a | --auto] [-b | --block] [-r | --rotation] [-d | --destination dest_id]

Usage: tmutil stopbackup

Usage: tmutil delete [-d backup_mount_point -t timestamp] [-p path]

Usage: tmutil deleteinprogress machine_directory

Usage: tmutil restore [-v] src ... dst

Usage: tmutil compare [-@acdefghlmnstuEX] [-D depth] [-I name]
       tmutil compare [-@acdefghlmnstuEX] [-D depth] [-I name] snapshot_path
       tmutil compare [-@acdefghlmnstuEUX] [-D depth] [-I name] path1 path2

Usage: tmutil setdestination [-a]  mount_point
       tmutil setdestination [-ap] afp://user[:pass]@host/share

Usage: tmutil removedestination destination_id

Usage: tmutil destinationinfo [-X]

Usage: tmutil addexclusion [-p|-v] item ...

Usage: tmutil removeexclusion [-p|-v] item ...

Usage: tmutil isexcluded item ...

Usage: tmutil inheritbackup machine_directory
       tmutil inheritbackup sparse_bundle

Usage: tmutil associatedisk [-a] mount_point volume_backup_directory

Usage: tmutil latestbackup [-t] [-d mount_point]

Usage: tmutil listbackups [-mt] [-d mount_point]

Usage: tmutil machinedirectory

Usage: tmutil calculatedrift machine_directory

Usage: tmutil uniquesize path ...

Usage: tmutil verifychecksums path ...

Usage: tmutil localsnapshot

Usage: tmutil listlocalsnapshots <mount_point>

Usage: tmutil listlocalsnapshotdates [<mount_point>]

Usage: tmutil deletelocalsnapshots [<mount_point> | <snapshot_date>]

Usage: tmutil thinlocalsnapshots <mount_point> [purgeamount] [urgency]

```