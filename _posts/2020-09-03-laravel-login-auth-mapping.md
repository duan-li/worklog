---
layout: post
title: Laravel login auth mapping
date: 2020-09-03 06:09 +0000
---

* [Laravel Multiple Guards Authentication: Setup and Login](https://medium.com/@sagarmaheshwary31/laravel-multiple-guards-authentication-setup-and-login-2761564da986)
* [How to Create a Custom Authentication Guard in Laravel](https://code.tutsplus.com/tutorials/how-to-create-a-custom-authentication-guard-in-laravel--cms-29667)


```mermaid
graph TB
A[app/LoginController] -- use --> B[Fund\Auth\AuthenticatesUsers]
B[Fund\Auth\AuthenticatesUsers] -- has --> C(login<> with $request)
B[Fund\Auth\AuthenticatesUsers] -- has --> D(attemptLogin<> with $request)
C(login<> with $request) -- call --> D(attemptLogin<> with $request)
B[Fund\Auth\AuthenticatesUsers] -- has --> E(credentials<> return array of username and password)
D(attemptLogin<> with $request) -- call --> F(Auth::guard<>)
F(Auth::guard<>) -- get --> G(guard instance)
G(guard instance) -- has --> H(attempt<>)
G(guard instance) -- call --> H(attempt<>)
```

