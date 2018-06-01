---
layout: post
title: "[HowTo]Mysql migration"
date: 2018-05-26 12:34 +0000
---

```
sudo docker run -it --rm -v /home/www-user/tmp:/backup dockercraft/mysql-client /bin/sh

```

```
mysqldump -u user_name -p -h from.server.ip --opt database_name > /backup/database_name-2018-05-26.sql

mysql -u user_name -p -h to.server.ip database_name < /backup/database_name-2018-05-26.sql


```



Ref:
 - https://www.digitalocean.com/community/tutorials/how-to-migrate-a-mysql-database-between-two-servers