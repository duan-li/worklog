---
layout: post
title: Laravel model
date: 2020-03-27 03:16 +0000
---


## Event
There are 3 events around a Model being saved in the database. [^1]

[^1]: [Eloquent model event are saved and created both called when create is used?](https://stackoverflow.com/questions/37158491/eloquent-model-event-are-saved-and-created-both-called-when-create-is-used)

* `created` is called when the model is saved for the first time.
* `updated` is called when the model is saved any subsequent time.
* `saved` is called any time the model is saved (including when it's first created).