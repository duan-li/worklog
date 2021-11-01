---
layout: post
title: MacOS time machine diagnostics
date: 2021-08-18 03:12 +0000
---

## Time Machine failing: “an error occurred while copying files” [^1]

[^1]: [Link](https://apple.stackexchange.com/questions/267790/time-machine-failing-an-error-occurred-while-copying-files)


```bash
log show --predicate 'subsystem == "com.apple.TimeMachine"' --info --last 4h|grep -i error

# or
log stream --level debug --predicate 'subsystem == "com.apple.TimeMachine"'
```


Hold down the `Option key` on the iMac while you click on the Time Machine "clock" icon at the top of the screen. Click **Verify Backups** to see if the procedure will run.

If no luck, hold down the `Shift key` on the iMac while you click on the Time Machine "clock" icon. Click **Back up with Consistency Scan** to see if things will run that way. [^2]

[^2]: [Apple support ticket](https://discussions.apple.com/thread/7862627)