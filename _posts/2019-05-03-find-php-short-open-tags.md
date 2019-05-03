---
layout: post
title: Find PHP short open tags
date: 2019-05-03 04:33 +0000
---

## Using PHPStorm[^phpstorm]
```bash
<\?(?!php|xml)
```

[^phpstorm]: [Finding all PHP short tags](https://stackoverflow.com/questions/6110932/finding-all-php-short-tags)


### Bash to find[^grep]
```bash
find -f ./ | grep -rn "<?[^p]\|<?$" *.php
```

[^grep]: [Finding PHP Short Tags](https://blog.josephscott.org/2010/06/28/finding-php-short-tags/)


[Replace PHP short open tags with full form in all '.php' files using one command](https://coderwall.com/p/cnm0_w/replace-php-short-open-tags-with-full-form-in-all-php-files-using-one-command)

---
