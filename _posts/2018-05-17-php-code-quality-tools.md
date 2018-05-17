---
layout: post
title: PHP code quality tools
date: 2018-05-17 14:45 +0000
---

* unit test (para)
* phpcs
* phpmd
* phpcpd
* phpstan

https://akrabat.com/checking-your-code-for-psr-2/

`phpcs --standard=PSR2 BaseApi.php`

docker run -it -v /Users/Duan/Code/lc/database/migrations:/lc phpcs --standard=PSR2 /lc/2018_05_17_113100_migrate_membership_do_not_share_offer_package.php



docker run -it -v /Users/Duan/Code/lc/database/migrations:/lc phpmd phpmd /lc/2018_05_17_113100_migrate_membership_do_not_share_offer_package.php codesize
