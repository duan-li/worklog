---
layout: post
title: jQuery HTML
date: 2019-07-31 09:44 +0000
---

## jQuery

### checkbox

**Is it checked**
```html
$('#myCheckbox').is(':checked')
```

**For jQuery 1.6+ :**

.attr() is deprecated for properties; use the new .prop() function instead as:

```html
$('#myCheckbox').prop('checked', true); // Checks it
$('#myCheckbox').prop('checked', false); // Unchecks it
```
**For jQuery < 1.6:**

To check/uncheck a checkbox, use the attribute checked and alter that. With jQuery you can do:
```html
$('#myCheckbox').attr('checked', true); // Checks it
$('#myCheckbox').attr('checked', false); // Unchecks it
```

Cause you know, in HTML, it would look something like:
```html
<input type="checkbox" id="myCheckbox" checked="checked" /> <!-- Checked -->
<input type="checkbox" id="myCheckbox" /> <!-- Unchecked -->
```
However, you cannot trust the .attr() method to get the value of the checkbox (if you need to). You will have to rely in the .prop() method. [^1]

[^1]: [check / uncheck checkbox using jquery?](https://stackoverflow.com/questions/17420534/check-uncheck-checkbox-using-jquery)


## Bootstrap

### modal

Prevent Bootstrap Modal from disappearing when clicking outside or pressing escape? [^2]

[^2]: [stack overflow](https://stackoverflow.com/questions/16152073/prevent-bootstrap-modal-from-disappearing-when-clicking-outside-or-pressing-esca)

```html
$('#myModal').modal({
    backdrop: 'static',
    keyboard: false
})
```
and in HTML:
```html
<a data-controls-modal="your_div_id" data-backdrop="static" data-keyboard="false" href="#">
```


---