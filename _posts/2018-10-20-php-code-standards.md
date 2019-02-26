---
layout: post
title: PHP Code Standards
date: 2018-10-10 06:05 +0000
---



# Extend [PSR-1](https://www.php-fig.org/psr/psr-1/) [RAW](https://raw.githubusercontent.com/php-fig/fig-standards/master/accepted/PSR-1-basic-coding-standard.md)
## 1. Overview
- Files MUST use only `<?php` tag only.


# [PSR-2](https://www.php-fig.org/psr/psr-2/) [RAW](https://raw.githubusercontent.com/php-fig/fig-standards/master/accepted/PSR-2-coding-style-guide.md)

This guide extends and expands on [PSR-1], the basic coding standard.

The intent of this guide is to reduce cognitive friction when scanning code from different authors. It does so by enumerating a shared set of rules and expectations about how to format PHP code.

The style rules herein are derived from commonalities among the various member projects. When various authors collaborate across multiple projects, it helps to have one set of guidelines to be used among all those projects. Thus, the benefit of this guide is not in the rules themselves, but in the sharing of those rules.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].


## 1. Overview
- Code MUST follow a "code style guide" PSR[PSR-1, PSR-2].
- File name MUST be case sensitive and MUST be `StudlyCaps`. File must be with `.php` (low case) at the end.
- File first line MUST be `<?php declare(strict_types=1);`, and MUST be one blank line after that.[^1]



[^1]: [14 Tips to Write PHP Code that is Hard to Maintain and Upgrade](https://www.tomasvotruba.cz/blog/2018/11/26/14-tips-to-write-php-code-that-is-hard-to-maintain-and-upgrade/)



## 2. Example

### Condition

```php
// this is wrong
if ($a == 1 or $b == 1) {

}

// this is correct
if ($a == 1 || $b == 1) {

}
```

```php
// this is wrong
if ($a == 1 and $b == 1) {

}

// this is correct
if ($a == 1 && $b == 1) {

}
```


```php
// this is wrong
if ($a == 1)
	doing($a)
else 
	dontDo($a)

// this is correct
if ($a == 1) {
	doing($a)
} else {
	dontDo($a)
}

```

#### `and` and `or`

```php
// this is wrong
if($a == 1 and $b == 1) {

}

if($a == 1 or $b == 1) {
	
}

```

```php
// this is correct
if($a == 1 && $b == 1) {

}

if($a == 1 || $b == 1) {
	
}

```

#### Early return 

```php
// this is wrong
function getX($condition) {
	
	if ($condition) {
		$a = 1;
	} else {
		$a = 2;
	}
	return $a;
}
```

**Return early**

```php
// this is correct
function getX($condition) {
	
	if ($condition) {
		return 1;
	}
	return 2;
}


```


### Comment
```
/**
 * Comment block format 
 * 
 */

// inline comment format

# this is wrong comment format, do not use it.

```

### Array

#### New array
```php
// create a new array.
$a = []; 

// old way, don't use it anymore
$a = array();

```

```php
// this is wrong
$a = [0 => 'a', 1 => 'b', 2 => 'c'];

// this is correct
$a = ['a', 'b', 'c'];
```


### Loop

#### `foreach` loop

```php
// this is wrong
foreach ($list as $item)
	doing($item)

// this is correct
foreach ($list as $item) {
	doing($item)
}

```

### String

```php
// do not use it anymore

$str1 = "this is";
$str2 = "woing ";

$string = $str1 . $str2;

// better to do this
$str1 = 'correct';
$string = sprintf("this is %s", $str1);
```


```php
$a = 'string';

$b = "this is $a";
```

---
