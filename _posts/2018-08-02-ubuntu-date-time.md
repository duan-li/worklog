---
layout: post
title: Ubuntu date time
date: 2018-08-02 10:10 +0000
---

## update timezone
```
sudo dpkg-reconfigure tzdata
```


## check NTP
```
timedatectl status
```

## turn on/off network time
```
sudo timedatectl set-ntp on|off
```



```
Warning: The system is configured to read the RTC time in the local time zone.
         This mode can not be fully supported. It will create various problems
         with time zone changes and daylight saving time adjustments. The RTC
         time is never updated, it relies on external facilities to maintain it.
         If at all possible, use RTC in UTC by calling
         'timedatectl set-local-rtc 0'.
```


```
502  sudo nano /etc/ntp.conf
  503  sudo service ntp restart
  504  timedatectl status
  505  sudo nano /etc/ntp.conf
  506  sudo service ntp restart
  507  udo dpkg-reconfigure
  508  sudo dpkg-reconfigure
  509  sudo dpkg-reconfigure time
  510  sudo dpkg-reconfigure date
  511  sudo dpkg-reconfigure
  512  sudo dpkg-reconfigure --info
  513  sudo timedatectl set-ntp on
  514  timedatectl status
  515  sudo timedatectl set-ntp off
  516  timedatectl status
  517  sudo timedatectl set-ntp no
  518  timedatectl status
  519  date
  520  date +%Y%m%d -s "20180718"
  521  sudo date +%Y%m%d -s "20180718"
  522  date
  523  hwclock --show
  524  sudo hwclock --show
  525  sudo hwclock --set --date="2018-07-19 16:45:05" --localtime
  526  sudo hwclock --show
  527  date
  528  sudo service ntp stop
  529  date
  530  sudo hwclock --set --date="2018-07-19 16:45:05" --localtime
  531  date
  532  timedatectl status
  533  sudo timedatectl set-local-rtc 0
  534  timedatectl status
  535  sudo service ntp start
  536  timedatectl status
  537  sudo service ntp stop
  538  timedatectl status
  539  sudo timedatectl set-local-rtc 0
  540  timedatectl status
  541  sudo service ntp stop
  542  sudo hwclock --set --date="2018-07-19 16:45:05" --localtime
  543  sudo service ntp stop
  544  timedatectl status
  545  date
  546  sudo timedatectl set-local-rtc 1
  547  date
  548  timedatectl status
  549  sudo hwclock --set --date="2018-07-19 16:45:05" --localtime
  550  timedatectl status
  551  sudo timedatectl set-local-rtc 0
  552  timedatectl status
  553  history
  554  sudo date +%Y%m%d -s "20180718"
  555  timedatectl status
  556  date
  557  history
```

