---
layout: post
title: Database pattern
date: 2018-05-22 09:34 +0000
---


# Do not use model on migrateion
Because model can be delete. It will brake migration

# Well know format status columns. 
Table status columns should using well-know format string like 'success' or 'fail', not 1 or 0. 

**Hard understand**
order_id | amount | status
------------ | -------------
1 | 200 | 1
2 | 100 | 2


**Easy understand**
order_id | amount | status
------------ | -------------
1 | 200 | paid
2 | 100 | completed


# view
View can be used only
* two entities have too many links between them.
* report

View can not be used if
* there is query apply to view.

View must has model, and modle must be read only.
