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


```bash
$ sudo apt docker.io docker-compose nfs-common portmap
```


## NFS
```bash
$ sudo mount -t nfs <ip>:/<dir> /mnt
```

In `/etc/fstab`, add 

```
<ip>:/<dir>		/home/user		nfs 	defaults	0	0
```

Options can be `nolock,nofail,x-systemd.automount,x-systemd.requires=network-online.target`. 


## Clean up

```bash
$ sudo apt purge vlc
$ sudo apt autoremove
$ sudo apt autoclean
$ sudo apt clean
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

