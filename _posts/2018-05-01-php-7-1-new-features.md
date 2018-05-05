---
layout: post
title: PHP 7.1 new features
date: 2018-05-01 10:10 +1000
---

## Nullable Types
```php
// return null|int
function checkAge($age): ?int
{
	if($age > 12){
		return $age;
	}else{
		return null; 
	}
}
```


## Void Function
```php
function setkey($key) : void // <-
{
	$this->key = $key;
}
```


## Symmetric Array Destructuring
```php
$data = [
	[1, 'TestB'],
	[2, 'TestC'],
];
[0,'TestA'] = $data[0];

foreach ($data as [$id, $name]) {
 // logic here with $id and $name
}

```

## Class Constant Visibility
```php
class ConstDemo
{
	const PUBLIC_CONST_A = 1;
	public const PUBLIC_CONST_B = 2;
	protected const PROTECTED_CONST = 3;
	private const PRIVATE_CONST = 4;
}
```

## Iterable Pseudo-type
```php
function iterator(iterable $iter)
{
	foreach ($iter as $val) {
		//
	}
}
```

## Multi Catch Exception Handling
```php
try {
	// some code
} catch (FirstException | SecondException | ThirdException $e) {
	// handle first and second exceptions
}

```

## Support for Keys In `list()`
```php
$data = [
	["id" => 1, "name" => 'Tom'],
	["id" => 2, "name" => 'Fred'],
];
// list() style
list("id" => $id1, "name" => $name1) = $data[0];
```



## Support for Negative String Offsets

```php
var_dump("abcdef"[-2]);
$string = 'bar';
echo "The last character of '$string' is '$string[-1]'.\n";
```

## Convert Callables to Closures
```php
class Calls
{
	public function showFunction()
	{
		return Closure::fromCallable([$this, 'privateFunction']);
	}

	private function callbackFunction($a,$b)
	{
		echo $a + $b;
	}
}

$privFunc = (new Calls)->showFunction();

$privFunc(1,2);
```

## Asynchronous Signal Handling
```php
pcntl_async_signals(true); // turn on async signals
pcntl_signal(SIGHUP, function($sig) {
	echo "SIGHUP\n";
});
posix_kill(posix_getpid(), SIGHUP);
```
## HTTP/2 server push support in `ext/curl`
PHP 7.1 `curl_multi_setopt()` add below
* CURLMOPT_PUSHFUNCTION
* CURL_PUSH_OK
* CURL_PUSH_DENY

## New Functions and Constants Introduced
* curl_multi_errno()
* curl_share_errno()
* curl_share_strerror()
* session_create_id()
* session_gc()

Besides functions, some new constants have also been introduced. They are:
* CURLMOPT_PUSHFUNCTION
* CURL_PUSH_OK
* CURL_PUSH_DENY
* FILTER_FLAG_EMAIL_UNICODE
* MT_RAND_PHP



https://www.cloudways.com/blog/whats-new-in-php-7-1/