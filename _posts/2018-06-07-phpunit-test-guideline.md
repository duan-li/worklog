---
layout: post
title: phpunit test guideline
date: 2018-06-07 11:32 +0000
---


# Pattern

use `DatabaseTransactions`. 


# Test case coverage

{% katex %}
(Code Coverage) = \frac{(Number of Lines of Code Called By Your Tests)}{(Total Number of Relevant Lines of Code)} * 100\%
{% endkatex %}



```
// Generate code coverage report in Clover HTML format.
phpunit --coverage-html <dir>

// Generate code coverage report in Clover XML format.
phpunit --coverage-clover <file>
```
Or using phpdbg, phpdbg can avoid Xdebug.


Ref
* https://github.com/framgia/laravel-test-guideline/blob/master/en/Introduction.md
* https://coveralls.io/pricing
* https://coderwall.com/p/mxtqiw/add-code-coverage-report-to-laravel-project
* https://hackernoon.com/generating-code-coverage-with-phpunite-and-phpdbg-4d20347ffb45