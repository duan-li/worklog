---
layout: post
title: phpunit test guideline
date: 2018-06-07 11:32 +0000
---


{% katex %}
(Code Coverage) = \frac{(Number of Lines of Code Called By Your Tests)}{(Total Number of Relevant Lines of Code)} * 100\%
{% endkatex %}



```
// Generate code coverage report in Clover HTML format.
phpunit --coverage-html <dir>

// Generate code coverage report in Clover XML format.
phpunit --coverage-clover <file>
```

Ref
* https://github.com/framgia/laravel-test-guideline/blob/master/en/Introduction.md
* https://coveralls.io/pricing