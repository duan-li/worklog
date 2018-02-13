---
layout: post
title: No Offset Query
date:   2018-02-12 11:06:03 +1000
categories: code
---

# Life With out Offset

```sql
SELECT *
FROM `table`
WHERE id < ?last_seen_id
ORDER BY id DESC
FETCH FIRST 10 ROWS ONLY
```

This approach—called seek method or keyset pagination—solves the problem of drifting results as illustrated above and is even faster than offset. 


# Keyset vs Offset

Offset instructs the databases skip the first N results of a query. However, the database must still fetch these rows from the disk and bring them in order before it can send the following ones.



[Slide](https://www.slideshare.net/MarkusWinand/p2d2-pagination-done-the-postgresql-way)
[No Offset](http://use-the-index-luke.com/no-offset)
