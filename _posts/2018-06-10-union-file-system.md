---
layout: post
title: Union file system
date: 2018-06-10 22:19 +0000
---

`copy-on-write` `CoW`.

# Advanced Multi-Layered Unification Filesystem
* image layer
* container layer 


## Image layer and AUFS
Docker image is maked by a group of read-only layer. Location is at `/var/lib/docker/aufs/diff`. And `/var/lib/docker/aufs/layers` stores metadata of image layer.


**Check `/var/lib/docker/aufs/diff`**
Dir is empty
I am image layer${n}


## Container layer and AUFS



## AUFS practice

**Create dirs and files**
```
# tree aufs/
aufs/
├── container-layer
│   └── container-layer.txt
├── image-layer1
│   └── image-layer1.txt
├── image-layer2
│   └── image-layer2.txt
├── image-layer3
│   └── image-layer3.txt
├── image-layer4
│   └── image-layer4.txt
└── mnt
```

**create container layer**
```
# cat aufs/container-layer/container-layer.txt
I am container layer
```

**create image layers**
```
# cat aufs/image-layer1/image-layer1.txt
I am image layer 1
# cat aufs/image-layer2/image-layer2.txt
I am image layer 2
# cat aufs/image-layer3/image-layer3.txt
I am image layer 3
# cat aufs/image-layer4/image-layer4.txt
I am image layer 4


```

**Mount AUFS**
```
/aufs# mount -t aufs -o dirs=./container-layer:./image-layer4:./image-layer3:./image-layer2:./image-layer1 none ./mnt
```

```
/aufs# tree mnt/
mnt/
├── container-layer.txt
├── image-layer1.txt
├── image-layer2.txt
├── image-layer3.txt
└── image-layer4.txt

0 directories, 5 files
```

**Permission**
```
/aufs# tree /sys/fs/aufs
/sys/fs/aufs
├── config
└── si_5116356d3ef6524b
    ├── br0
    ├── br1
    ├── br2
    ├── br3
    ├── br4
    ├── brid0
    ├── brid1
    ├── brid2
    ├── brid3
    ├── brid4
    └── xi_path

1 directory, 12 files
```


```
/aufs# cat /sys/fs/aufs/si_5116356d3ef6524b/*
/root/aufs/container-layer=rw
/root/aufs/image-layer4=ro
/root/aufs/image-layer3=ro
/root/aufs/image-layer2=ro
/root/aufs/image-layer1=ro
64
65
66
67
68
/root/aufs/container-layer/.aufs.xino
```

**Test write**
```
/aufs# echo -e "\nwrite to mnt's image-layer1.txt" >> mnt/image-layer4.txt
root@ubuntu-s-1vcpu-1gb-sgp1-01:~/aufs# cat mnt/image-layer4.txt
I am image layer 4

write to mnt's image-layer1.txt


/aufs# cat image-layer4/image-layer4.txt
I am image layer 4


/aufs/container-layer# ls
container-layer.txt  image-layer1.txt  image-layer4.txt
```

