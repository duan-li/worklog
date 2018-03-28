---
layout: page
title: Carbon
---

## Initial

`Carbon::createFromFormat('Y-m-d H:i:s', session()->get('auth_google_login'));`

`Carbon::now();`

https://carbon.nesbot.com/docs/

## Unit test
```php
$now = \Carbon\Carbon::create(2020,01, 12, 01, 01, 01);
\Carbon\Carbon::setTestNow($now);
```

## Date/Time Format

Day Character | Example 
--- | --- 
d | 01-31
D | Mon to Sun
j | 1-31
l (lowercase L) | Sunday to Saturday
N | 1-7 (Mon to Sun)
S | st, nd, rd or th.
w | 0-6 (Sun to Sat)
z | 0-365

Week Character | Example 
--- | --- 
W | 1-42 42 weeks

Month Character | Example 
--- | --- 
F | January to December
m | 01 to 12
M | Jan to Dec
n | 1 to 12
t | 28 to 31

Year Character | Example 
--- | --- 
L | 1 for leap, 0 otherwise
o | 2018
Y | same as o
y | 98 or 99

Time Character | Example 
--- | --- 
a | am/pm
A | AM/PM
B | internet time 000 to 999
g | 1-12 hour
G | 0-23 hour
h | 01 to 12
H | 00 to 23
i | 00 to 59 minutes
s | 00 to 59 seconds
u | Microseconds 6 digital
v | Microseconds 3 digital


Ref:
http://php.net/manual/en/function.date.php