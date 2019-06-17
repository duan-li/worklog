---
layout: post
title: php execute linux shell command
date: 2019-01-08 14:08 +0000
---

- `exec` : returns the last line of the output by default, but can provide all output as an array specifed as the second parameter.
- `shell_exec` : returns all of the output stream as a string. [^1]
- `system()` : displays output directly without using echo or print. [^2]
- `passthru()` : when the output from the Unix command is binary data [^3]
- `proc_open()`: proc_open — Execute a command and open file pointers for input/output [^4]

The error data is output from the target program's STDERR stream. You can get access to the error data through the normal returned string from shell_exec() by appending `2>&1` to the command, which will redirect STDERR to STDOUT, the stream that you are currently seeing. [^5]

```php
var_dump(shell_exec("ffmpeg -i /var/www/html/sitedomain/httpdocs/tmp/ebev1177.mp4 2>&1"));
```

```php
$cwd='/tmp';
$descriptorspec = array(
//	0 => array("pipe", "r"),
	1 => array("pipe", "w"),
	2 => array("pipe", "w") );

$process = proc_open("php1 -v", $descriptorspec, $pipes, $cwd);
echo "stdout\n";

$stdout = stream_get_contents($pipes[1]);
var_dump($stdout); 
fclose($pipes[1]);

echo "stderr\n";
$stderr = stream_get_contents($pipes[2]);
var_dump($stderr);
fclose($pipes[2]);
```

[^1]: [PHP shell_exec vs exec](https://stackoverflow.com/questions/7093860/php-shell-exec-vs-exec)

[^2]: [How To Execute Shell Commands with PHP Exec and Examples](https://www.poftut.com/execute-shell-commands-php-exec-examples/)

[^3]: [function.passthru.php](http://php.net/manual/en/function.passthru.php)

[^4]: [proc_open](https://php.net/proc-open)

[^5]: [PHP - How to get Shell errors echoed out to screen](https://stackoverflow.com/questions/15086572/php-how-to-get-shell-errors-echoed-out-to-screen)
---