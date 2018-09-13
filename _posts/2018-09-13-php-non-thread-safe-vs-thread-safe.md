---
layout: post
title: PHP non-thread safe vs thread safe
date: 2018-09-13 16:44 +0000
---

Detail | Non thread safe | thread safe
------------ | ------------ | -------------
Thread | single thread is used | multi-processing
Env | CGI binary, command line  | env need multiple PHP threads
Web server | Nginx/Lighttpd | Apache MPM


## What are they

>Since with mod_php, PHP gets loaded right into Apache, if Apache is going to handle concurrency using its Worker MPM (that is, using Threads) then PHP must be able to operate within this same multi-threaded environment -- meaning, PHP has to be thread-safe to be able to play ball correctly with Apache! [^1]

[^1]: [What is thread safe or non-thread safe in PHP?](https://stackoverflow.com/questions/1623914/what-is-thread-safe-or-non-thread-safe-in-php)

---
