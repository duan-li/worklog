---
layout: post
title: Docker in Raspberry Pi 3
date: 2018-12-27 12:08 +0000
---

## Remove Docker 1.8
```bash
apt-get remove docker.io
apt-get autoremove
apt-get clean
```


## Install 3rd-party docker
Install docker-hypriot [^1]

[^1]: [tyrell/docker-install-rpi3.md](https://gist.github.com/tyrell/2963c6b121f79096ee0008f5a47cf347)


```bash
sudo apt-get install -y apt-transport-https

wget -q https://packagecloud.io/gpg.key -O - | sudo apt-key add -

echo 'deb https://packagecloud.io/Hypriot/Schatzkiste/debian/ wheezy main' | sudo tee /etc/apt/sources.list.d/hypriot.list

sudo apt-get update

sudo apt-get install -y docker-hypriot

sudo systemctl enable docker
```


## Fix permission issue

Change `docker.sock` owner
```bash
sudo chown pi:docker /var/run/docker.sock
```
Or following add user to `docker` group [^2]
```bash
sudo gpasswd -a ${USER} docker
```
[^2]: https://blog.csdn.net/xiojing825/article/details/79494408







---
