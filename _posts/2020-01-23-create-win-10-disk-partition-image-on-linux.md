---
layout: post
title: Create Win 10 disk partition image on Linux
date: 2020-01-23 02:27 +0000
---


## Backup MBR

```bash
dd if=/dev/sda of=/boot/boot.NNNN bs=512 count=1
```

## Recovery MBR

```bash
dd if=/boot/boot.NNNN of=/dev/sda bs=512 count=1
```

If want keep DPT, change `bs=512` to `bs=446`. [^dpt]

[^dpt]: https://blog.csdn.net/xiongyangg/article/details/20629737


 - [Clonezilla](https://clonezilla.org/), [tutorial](https://kknews.cc/tech/x5yaalq.html)
 - [fdisk and dd](https://fooyou.github.io/document/2015/10/10/using-dd-as-ghost-on-linux.html)