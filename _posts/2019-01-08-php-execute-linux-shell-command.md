---
layout: post
title: php execute linux shell command
date: 2019-01-08 14:08 +0000
---

- `exec` : returns the last line of the output by default, but can provide all output as an array specifed as the second parameter.
- `shell_exec` : returns all of the output stream as a string. [^1]
- `system()` : displays output directly without using echo or print. 
- `passthru()` : when the output from the Unix command is binary data [^3]

[^1]: [PHP shell_exec vs exec](https://stackoverflow.com/questions/7093860/php-shell-exec-vs-exec)

[^2]: [How To Execute Shell Commands with PHP Exec and Examples](https://www.poftut.com/execute-shell-commands-php-exec-examples/)

[^3]: [function.passthru.php](http://php.net/manual/en/function.passthru.php)

---