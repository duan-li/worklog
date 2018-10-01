---
layout: post
title: Bug Mailer
date: 2018-09-11 09:53 +0000
---

## Design

### Env:
* Production
* staging
* local (default)
* customize. will follow setting of local


### Email
* from
* title format



```php
Facade::reportError(); call bugMailer->report($e, 'error');
Facade::reportWarning(); call bugMailer->report($e, 'warning');
Facade::reportInfo(); call bugMailer->report($e, 'info');
Facade::report($e, $level) call bugMailer->report($e, $level);

```  


## Example
### Laravel 5.x Email Exceptions [^1]

[^1]: [github](https://github.com/abrigham1/laravel-email-exceptions)

#### PROS
* Good email template
* Good config structure
* Supports throttle


#### CONS
* No facade avaiable  
* No email group (list), mutiple emails




---
