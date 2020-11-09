---
layout: post
title: Quick setup Pi
date: 2020-01-14 03:47 +0000
---

## Initial

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt dist-upgrade
$ sudo rpi-update
```

## Wifi [^wifi]

[^wifi]: [How to auto-connect your Raspberry Pi to a hidden SSID wifi network](https://raspi.tv/2017/how-to-auto-connect-your-raspberry-pi-to-a-hidden-ssid-wifi-network)

`sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=AU
 
network={
        scan_ssid=1
        ssid="hidden_SSID_here"
        psk="password_here"
        key_mgmt=WPA-PSK
}
```

## Config

```bash
$ sudo raspi-config
```

Enable 
 - 5 Interfacing Options > SSHd
 - 5 Interfacing Options > VNC
 - 2 Network options > B2 Wait for network at Boot

## Install

For old system

```bash
sudo apt install docker.io docker-compose nfs-common portmap
```

For new system

```bash
sudo apt install docker.io docker-compose gnupg2 pass -y
```


## NFS
```bash
$ sudo mount -t nfs <ip>:/<dir> /mnt
```

### Copy file [^cp]

[^cp]: [How to copy with cp to include hidden files and hidden directories and their contents?](https://superuser.com/questions/61611/how-to-copy-with-cp-to-include-hidden-files-and-hidden-directories-and-their-con)

```bash
$ cp -rT /home/usr /mnt
```


### Update fstab, mount NFS when boot

In `/etc/fstab`, add 

```
<ip>:/<dir>		/home/user		nfs 	defaults	0	0
```

Options can be `nolock,nofail,x-systemd.automount,x-systemd.requires=network-online.target`. 


## PHP [^php]

[^php]: [Installing PHP7.4 on a Rapsberry Pi](https://janw.me/2019/installing-php7-4-rapsberry-pi/)

```bash
sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ buster main" | sudo tee /etc/apt/sources.list.d/php.list
sudo apt update
```

```bash

sudo apt install php7.3 \
	php7.3-bcmath \
	php7.3-bz2 \
	php7.3-cli \
	php7.3-common \
	php7.3-curl \
	php7.3-gd \
	php7.3-gmp \
	php7.3-imap \
	php7.3-intl \
	php7.3-json \
	php7.3-ldap \
	php7.3-mbstring \
	php7.3-mysql \
	php7.3-opcache \
	php7.3-readline \
	php7.3-recode \
	php7.3-snmp \
	php7.3-soap \
	php7.3-sqlite3 \
	php7.3-tidy \
	php7.3-xml \
	php7.3-xmlrpc \
	php7.3-xsl \
	php7.3-zip \
	composer -y
```


## Clean up

```bash
sudo apt purge vlc
sudo apt autoremove
sudo apt autoclean
sudo apt clean
```


## Battery

8:08am until 21:28, Unknown capbility, likely 6000mAh.

## Hardware detail

`vcgencmd` [^vcgencmd]

[^vcgencmd]: [RPI vcgencmd usages](https://elinux.org/RPI_vcgencmd_usage)

```bash
cat /sys/class/thermal/thermal_zone0/temp 
/opt/vc/bin/vcgencmd measure_temp
/opt/vc/bin/vcgencmd measure_volts
```

* [Software Monitoring of Supply Voltage and CPU Temperature](https://www.raspberrypi.org/forums/viewtopic.php?t=30697)
* [RPi CPU temp with Python](https://www.raspberrypi.org/forums/viewtopic.php?t=185244)

