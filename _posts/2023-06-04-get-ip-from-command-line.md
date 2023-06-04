---
layout: post
title: Get IP from command line
date: 2023-06-04 11:27 +0000
---

```bash
dig -4 TXT +short o-o.myaddr.l.google.com @ns1.google.com
```

or 

```bash
curl -s http://checkip.dyndns.org/ | sed 's/[a-zA-Z<>/ :]//g'
```