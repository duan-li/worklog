---
layout: post
title: Chrome headless
date: 2019-01-07 15:44 +0000
---

## Mac OS [^1]

[^1]: [How to Use Headless Chrome on Apple OSX](https://medium.com/@anotherplanet/how-to-use-headless-chrome-on-apple-osx-d9f7f3a54983)

```
alias chrome="/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome"
```

## chrome headless

`--virtual-time-budget` is to delay loading [^2]

[^2]: [Make Chrome Headless to Wait for Ajax Before Printing to PDF](https://stackoverflow.com/questions/49614437/make-chrome-headless-to-wait-for-ajax-before-printing-to-pdf)



```bash
chrome --headless --disable-gpu --print-to-pdf --virtual-time-budget=99999999 --run-all-compositor-stages-before-draw https://shop.coles.com.au/a/a-vic-metro-burwood-east/product/nan-optipro--ha-gold-formula-stage-1

chrome --headless --disable-gpu --dump-dom --virtual-time-budget=99999999 --run-all-compositor-stages-before-draw https://shop.coles.com.au/a/a-vic-metro-burwood-east/product/nan-optipro--ha-gold-formula-stage-1

chrome --headless http://localhost:8080/banana/key --run-all-compositor-stages-before-draw --print-to-pdf=C:\tmp\tmp.pdf --virtual-time-budget=10000
```

### linux
```
chromium-browser --headless --dump-dom --disable-gpu --virtual-time-budget=9000000 --run-all-compositor-stages-before-draw https://shop.coles.com.au/a/a-vic-metro-burwood-east/product/nan-optipro--ha-gold-formula-stage-1
```

---