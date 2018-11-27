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



---
