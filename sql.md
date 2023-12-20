---
layout: page
title: SQL
---

Check if null

`ifnull(name, 'NULL') as name,`

https://stackoverflow.com/questions/806989/how-to-find-all-tables-that-have-foreign-keys-that-reference-particular-table-co

```sql
USE information_schema;
SELECT *
FROM
  KEY_COLUMN_USAGE
WHERE
  REFERENCED_TABLE_NAME = 'X'
  AND REFERENCED_COLUMN_NAME = 'X_id';

```


```sql
SELECT *
FROM
  KEY_COLUMN_USAGE
WHERE
  REFERENCED_TABLE_NAME = 'X'
  AND REFERENCED_COLUMN_NAME = 'X_id'
  AND TABLE_SCHEMA = 'your_database_name';

```

**check duplicate column**
`SELECT column_name, COUNT(*) c FROM tables GROUP BY column_name HAVING c > 1`


**selecting the last records in a one-to-many relationship**
```
SELECT c.*, p1.*
FROM customer c
JOIN purchase p1 ON (c.id = p1.customer_id)
LEFT OUTER JOIN purchase p2 ON (c.id = p2.customer_id AND 
    (p1.date < p2.date OR p1.date = p2.date AND p1.id < p2.id))
WHERE p2.id IS NULL;
```
