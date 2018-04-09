---
layout: post
title: PHP Bitmask
date: 2018-04-09 10:07 +1000
---

```php
const FLAG_1 = 0b0001; // 1
const FLAG_2 = 0b0010; // 2
const FLAG_3 = 0b0100; // 4
const FLAG_4 = 0b1000; // 8
// Can you see the pattern? ;-)

function show_flags ($flags) {
  if ($flags & FLAG_1) {
    echo "You passed flag 1!<br>\n";
  }
  if ($flags & FLAG_2) {
    echo "You passed flag 2!<br>\n";
  }
  if ($flags & FLAG_3) {
    echo "You passed flag 3!<br>\n";
  }
  if ($flags & FLAG_4) {
    echo "You passed flag 4!<br>\n";
  }
}

show_flags(FLAG_1 | FLAG_3);
```


(Demo)[https://3v4l.org/tTZnW#output]



```php

const TYPE_1 = 1;
const TYPE_2 = 2;
const TYPE_3 = 4;

$type = 0;

function setType($setType)
{
	$type |= $setType;
}

function showType($type)
{
	if($type & TYPE_1) {
		echo 'type is 1';
	}

	if($type & TYPE_2) {
		echo 'type is 2';
	}

	if($type & TYPE_3) {
		echo 'type is 3';
	}
}

```