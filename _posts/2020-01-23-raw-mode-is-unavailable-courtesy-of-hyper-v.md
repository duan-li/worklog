---
layout: post
title: Raw-mode is unavailable courtesy of Hyper-V
date: 2020-01-23 00:20 +0000
---


Result Code: | E_FAIL (0x80004)
-- | --
Component: | ConsoleWrap
Interface: | IConsole {872da645-bee2}

```
Raw-mode is unavailable courtesy of Hyper-V. (VERR_SUPDRV_NO_RAW_MODE_HYPER_V_ROOT).

Result Code: 
E_FAIL (0x80004)
Component: 
ConsoleWrap
Interface: 
IConsole {872da645-bee2}
```

```bash

#turn off
bcdedit /set hypervisorlaunchtype off

#turn on
bcdedit /set hypervisorlaunchtype auto

```