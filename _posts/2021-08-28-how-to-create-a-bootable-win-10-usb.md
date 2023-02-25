---
layout: post
title: How to Create a Bootable Win 10 USB
date: 2021-08-28 23:35 +0000
categories: [System]
tags: [Windows]
---

Booting Windows from a USB device provides flexibility, enables troubleshooting and repairs, facilitates system installations and upgrades, and allows for testing and data recovery. It offers an alternative way to access and work with Windows, especially in situations where the computer's internal storage or operating system is unavailable or problematic.

## Requirements

**USB device**
You will need a USB device (such as a USB flash drive) with sufficient storage capacity to hold the Windows installation files. Make sure the USB device is empty or does not contain any important data, as the process will erase its contents.


**Windows ISO**
Obtain a Windows ISO file from the official Microsoft website or other legitimate sources. The ISO file contains the complete installation media for the specific version and edition of Windows you want to install or use for booting.

**Setting**
Before booting from the USB device, you may need to adjust the BIOS or UEFI settings on your computer. The specific steps to access these settings and change the boot order may vary depending on your computer's manufacturer and model.



## Create From Windows

You can use *[Media Creation Tool](https://www.windowscentral.com/how-create-windows-10-usb-bootable-media-uefi-support)* to create a bootable USB drive with Windows 10 installation files. The tool is available from Microsoft's official website.


### rufus tools

If you can't create a bootable USB drive by *Media Creation Tool*, you can try *rufus*. [Rufus](https://rufus.ie/) is a popular and widely used utility for creating bootable USB drives. It is a free and open-source tool that allows you to easily create bootable USB devices from ISO files, including Windows installation media and various other operating systems or software. 

Rufus is compatible with Windows operating systems and is a popular choice among users who need to create bootable USB drives for various purposes, including installing operating systems, running live environments, upgrading firmware, and more.

Please note that when using Rufus or any other tool to create bootable USB drives, it's important to obtain ISO files from official and trusted sources to ensure the integrity and security of the files being used.



## From linux

- [How to Easily Create Windows 10 Bootable USB on Ubuntu or Any Linux Distro](https://www.linuxbabe.com/ubuntu/easily-create-windows-10-bootable-usb-ubuntu)
  - GUI and command line
- [How to Create a Bootable Windows 10 USB in Linux](https://itsfoss.com/bootable-windows-usb-linux/)
  - GUI
- [Create a Bootable Windows 10 USB in Linux With Ubuntu/Debian GUI](https://www.cyberciti.biz/faq/create-a-bootable-windows-10-usb-in-linux/)



## From MacOS - Never working for UEFI

- [How to Make a Windows 10 USB Using Your Mac - Build a Bootable ISO From Your Mac's Terminal](freecodecamp.org/news/how-make-a-windows-10-usb-using-your-mac-build-a-bootable-iso-from-your-macs-terminal/)