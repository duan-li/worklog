---
layout: post
title: "[HowTo]Mysql docker"
date: 2018-05-23 09:34 +0000
---

```
sudo docker run -it --rm -v ./mysql:/mysql mysql:5.6 /bin/bash
sudo docker run -it --rm -v /home/www-user/mysql:/mysql mysql:5.6 /bin/bash
sudo docker run -d --rm -v /home/www-user/mysql:/var/lib/mysql mysql:5.6 /bin/bash
sudo docker run -it --rm -v /home/www-user/mysql:/mysql -v /home/www-user/etc/mysql:/etc-mysql mysql:5.6 /bin/bash
sudo docker run -d --rm -v /home/www-user/mysql:/mysql -v /home/www-user/etc/mysql:/etc/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=simplepassword mysql:5.6

```


Try 1: this on working but cant back db dir `mysql`
```
rm -R /home/www-user/mysql
mkdir /home/www-user/mysql
sudo docker run -it --rm -v /home/www-user/mysql:/var/lib/mysql -v /home/www-user/nginx-php-mysql/mysql:/etc-mysql mysql:5.6 /bin/bash
# below is working
sudo docker run -d --rm -v /home/www-user/mysql:/mysql -v /home/www-user/nginx-php-mysql/mysql:/etc/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=simplepassword mysql:5.6
```

Try 2
```
sudo docker run -it --rm -v /home/www-user/mysql:/var/lib/mysql -v /home/www-user/nginx-php-mysql/mysql:/etc/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=simplepassword mysql:5.6 /bin/sh
#su mysql
#bash
#sudo /usr/sbin/mysqld &
```

Try 3 working good
```
sudo docker run -d --rm -v /home/www-user/mysql:/var/lib/mysql -v /home/www-user/nginx-php-mysql/mysql:/etc/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=simplepassword mysql:5.6
```


# How To
```
sudo docker run -d --rm -v /home/www-user/mysql:/var/lib/mysql -v /home/www-user/nginx-php-mysql/mysql:/etc/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=simplepassword mysql:5.6

```


# Optimize
optimize mysql performation with mysqltuner


```
wget http://mysqltuner.pl/ -O mysqltuner.pl
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/basic_passwords.txt -O basic_passwords.txt
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/vulnerabilities.csv -O vulnerabilities.csv


```

```
 >>  MySQLTuner 1.7.9 - Major Hayden <major@mhtx.net>
 >>  Bug reports, feature requests, and downloads at http://mysqltuner.com/
 >>  Run with '--help' for additional options and output filtering

[--] Skipped version check for MySQLTuner script
[--] Performing tests on 127.0.0.1:3306
[OK] Logged in using credentials passed on the command line
[OK] Currently running supported MySQL version 5.6.40
[OK] Operating on 64-bit architecture

-------- Log file Recommendations ------------------------------------------------------------------
[--] Log file: /var/lib/mysql/67a789e593ef.err(0B)
[!!] Log file /var/lib/mysql/67a789e593ef.err doesn't exist
[!!] Log file /var/lib/mysql/67a789e593ef.err isn't readable.

-------- Storage Engine Statistics -----------------------------------------------------------------
[--] Status: +ARCHIVE +BLACKHOLE +CSV -FEDERATED +InnoDB +MEMORY +MRG_MYISAM +MyISAM +PERFORMANCE_SCHEMA
[--] Data in InnoDB tables: 752K (Tables: 5)
[OK] Total fragmented tables: 0

-------- Security Recommendations ------------------------------------------------------------------
[OK] There are no anonymous accounts for any database users
[OK] All database users have passwords assigned
[!!] User 'root@%' hasn't specific host restriction.
[--] There are 612 basic passwords in the list.

-------- CVE Security Recommendations --------------------------------------------------------------
[OK] NO SECURITY CVE FOUND FOR YOUR VERSION

-------- Performance Metrics -----------------------------------------------------------------------
[--] Up for: 4h 23m 1s (31 q [0.002 qps], 21 conn, TX: 57K, RX: 3K)
[--] Reads / Writes: 100% / 0%
[--] Binary logging is disabled
[--] Physical Memory     : 3.9G
[--] Max MySQL memory    : 742.8M
[--] Other process memory: 138.9M
[--] Total buffers: 169.0M global + 1.1M per thread (151 max threads)
[--] P_S Max memory usage: 403M
[--] Galera GCache Max memory usage: 0B
[OK] Maximum reached memory usage: 575.2M (14.58% of installed RAM)
[OK] Maximum possible memory usage: 742.8M (18.83% of installed RAM)
[OK] Overall possible memory usage with other process is compatible with memory available
[OK] Slow queries: 0% (0/31)
[OK] Highest usage of available connections: 1% (2/151)
[!!] Aborted connections: 57.14%  (12/21)
[!!] name resolution is active : a reverse name resolution is made for each new connection and can reduce performance
[!!] Query cache may be disabled by default due to mutex contention.
[!!] Query cache efficiency: 0.0% (0 cached / 9 selects)
[OK] Query cache prunes per day: 0
[OK] Sorts requiring temporary tables: 0% (0 temp sorts / 1 sorts)
[OK] No joins without indexes
[!!] Temporary tables created on disk: 40% (6 on disk / 15 total)
[OK] Thread cache hit rate: 90% (2 created / 21 connections)
[OK] Table cache hit rate: 90% (66 open / 73 opened)
[OK] Open file limit used: 0% (18/1M)
[OK] Table locks acquired immediately: 100% (71 immediate / 71 locks)

-------- Performance schema ------------------------------------------------------------------------
[--] Memory used by P_S: 403.9M
[--] Sys schema isn't installed.

-------- ThreadPool Metrics ------------------------------------------------------------------------
[--] ThreadPool stat is disabled.

-------- MyISAM Metrics ----------------------------------------------------------------------------
[!!] Key buffer used: 18.2% (1M used / 8M cache)
[OK] Key buffer size / total MyISAM indexes: 8.0M/2.5M

-------- InnoDB Metrics ----------------------------------------------------------------------------
[--] InnoDB is enabled.
[--] InnoDB Thread Concurrency: 0
[OK] InnoDB File per table is activated
[OK] InnoDB buffer pool / data size: 128.0M/752.0K
[!!] Ratio InnoDB log file size / InnoDB Buffer pool size (75 %): 48.0M * 2/128.0M should be equal 25%
[!!] InnoDB buffer pool <= 1G and Innodb_buffer_pool_instances(!=1).
[--] InnoDB Buffer Pool Chunk Size not used or defined in your version
[!!] InnoDB Read buffer efficiency: 82.05% (882 hits/ 1075 total)
[!!] InnoDB Write Log efficiency: 0% (1 hits/ 0 total)
[OK] InnoDB log waits: 0.00% (0 waits / 1 writes)

-------- AriaDB Metrics ----------------------------------------------------------------------------
[--] AriaDB is disabled.

-------- TokuDB Metrics ----------------------------------------------------------------------------
[--] TokuDB is disabled.

-------- XtraDB Metrics ----------------------------------------------------------------------------
[--] XtraDB is disabled.

-------- RocksDB Metrics ---------------------------------------------------------------------------
[--] RocksDB is disabled.

-------- Spider Metrics ----------------------------------------------------------------------------
[--] Spider is disabled.

-------- Connect Metrics ---------------------------------------------------------------------------
[--] Connect is disabled.

-------- Galera Metrics ----------------------------------------------------------------------------
[--] Galera is disabled.

-------- Replication Metrics -----------------------------------------------------------------------
[--] Galera Synchronous replication: NO
[--] No replication slave(s) for this server.
[--] Binlog format: STATEMENT
[--] XA support enabled: ON
[--] Semi synchronous replication Master: Not Activated
[--] Semi synchronous replication Slave: Not Activated
[--] This is a standalone server

-------- Recommendations ---------------------------------------------------------------------------
General recommendations:
    Restrict Host for user@% to user@SpecificDNSorIp
    MySQL started within last 24 hours - recommendations may be inaccurate
    Reduce or eliminate unclosed connections and network issues
    Configure your accounts with ip or subnets only, then update your configuration with skip-name-resolve=1
    When making adjustments, make tmp_table_size/max_heap_table_size equal
    Reduce your SELECT DISTINCT queries which have no LIMIT clause
    Consider installing Sys schema from https://github.com/mysql/mysql-sys
    Read this before changing innodb_log_file_size and/or innodb_log_files_in_group: http://bit.ly/2wgkDvS
Variables to adjust:
    query_cache_size (=0)
    query_cache_type (=0)
    query_cache_limit (> 1M, or use smaller result sets)
    tmp_table_size (> 16M)
    max_heap_table_size (> 16M)
    innodb_log_file_size should be (=16M) if possible, so InnoDB total log files size equals to 25% of buffer pool size.
    innodb_buffer_pool_instances (=1)
```

https://dba.stackexchange.com/questions/70036/good-configuration-for-2gb-my-cnf
https://www.faqforge.com/linux/optimize-mysql-performance-with-mysqltuner/
https://github.com/major/MySQLTuner-perl
https://www.linode.com/docs/databases/mysql/how-to-optimize-mysql-performance-using-mysqltuner/
