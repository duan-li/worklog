---
layout: post
title: Linux system clean up
date: 2020-04-02 21:57 +0000
---

## Ubuntu/Debian apt
```bash
apt-get clean && rm -rf /var/lib/apt/lists/*
```

## General Linux

### System 

```bash
rm -Rf /tmp && mkdir /tmp
rm -Rf $HOME/.cache
```

### Conda

```bash
conda clean --all -f -y
```


## Alpine Linux

```bash
rm -rf /var/cache/apk/*
```

## CentOs/Red hat Linux

```bash
yum clean all
```


## Tips reduce docker image size

* [Tips to Reduce Docker Image Sizes](https://hackernoon.com/tips-to-reduce-docker-image-sizes-876095da3b34)
* [Docker Images : Part I - Reducing Image Size](https://www.ardanlabs.com/blog/2020/02/docker-images-part1-reducing-image-size.html)
* [How to reduce Docker Image sizes using multi-stage builds](https://blog.logrocket.com/reduce-docker-image-sizes-using-multi-stage-builds/)
