---
layout: post
title: "[SQL] Deleting and updating data from multiple related tables(On Delete)"
date: 2018-04-17 09:47 +1000
---

# On Delete
 - Set null
 - Cascade
 - No action
 - Restricct

ON DELETE CASCADE, means when you run a DELETE statement on a parent table it will DELETE all the corresponding rows from the CHILD table automatically, but the RESTRICT (which is the default foreign key relationship behavior) is when you try to delete a row from the parent table and there is a row in the child table with the same Id, it will fail complaining about the existing child rows.


# On Update
 - Set null
 - Cascade
 - No action
 - Restricct