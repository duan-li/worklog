---
layout: post
title: Make product import easy
date: 2018-05-08 11:47 +0000
---

```mermaid
graph LR


C((CSV)) -- Input --> I(Importer)
TM((Tag mapping)) -- Input --> I(Importer)
CM((Category mapping)) -- Input --> I(Importer)
DM((DB column mapping)) -- Input --> I(Importer)

I(Importer) -- Write --> P[Product DB]
I(Importer) -- Write --> L[Log DB]
```