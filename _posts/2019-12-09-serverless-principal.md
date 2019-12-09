---
layout: post
title: Serverless principal
date: 2019-12-09 20:58 +0000
---

1. There are at least one task need to be done when certain events occur. (Event driven)
2. We do nothing until event occur. (No deamon)
3. People can wait until tasks have been done. (Queue)


```php
interface Event
{
	public function get();
}
```


```php
interface EventHandler
{
	public function handler(Event $event);
}
```
