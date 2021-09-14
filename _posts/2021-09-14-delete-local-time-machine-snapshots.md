---
layout: post
title: Delete local Time Machine snapshots
date: 2021-09-14 11:36 +0000
---


```bash

# list all local snapshots
tmutil listlocalsnapshots /

# delete snapshot by date
sudo tmutil deletelocalsnapshots 2020-10–09-002010

```

[How to fix “Not enough free space to install Big Sur” error](https://macpaw.com/how-to/not-enough-space-to-install-big-sur)


## Usage

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