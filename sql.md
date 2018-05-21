---
layout: page
title: SQL
---

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