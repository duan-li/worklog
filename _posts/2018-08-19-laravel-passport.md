---
layout: post
title: Laravel passport
date: 2018-08-19 11:58 +0000
---




## Prepare
If it's new laravel project and you are running mysql < 5.7. You [need fix this](https://laravel-news.com/laravel-5-4-key-too-long-error).
```
composer require laravel/passport

php artisan migrate

```


## Install
```
# php artisan passport:install
Encryption keys generated successfully.
Personal access client created successfully.
Client ID: 1
Client Secret: nWOb11IanX2wtY4so8JxeSveSxzO6Mqvy6y45qlr
Password grant client created successfully.
Client ID: 2
Client Secret: wx9pntlhhytymMySjZAReS4Vx11RH4qlpNWOlLQo
```

## Config and Setup
* [ ] TODO

## Publish components
```
$ php artisan vendor:publish --tag=passport-components
Copied Directory [/vendor/laravel/passport/resources/assets/js/components] To [/resources/assets/js/components/passport]
Publishing complete.
```

## Issue Tokens
There are two ways to issue token.
* console command
* Json API

