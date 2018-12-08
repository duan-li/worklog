---
layout: post
title: Run bash script in Windows 10
date: 2018-12-08 15:39 +0000
---

```bash
@ECHO OFF
setlocal DISABLEDELAYEDEXPANSION
SET BIN_TARGET=%~dp0/../agilekeys/cans/bin/cans
bash "%BIN_TARGET%" %*
```

---
