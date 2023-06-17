---
layout: post
title: No Offset Query
date:   2018-02-12 11:06:03 +1000
categories: [Code]
tags: [SQL, Offset, Keyset]
---

## What is Offset in SQL query

In SQL, the OFFSET clause is used to skip a specified number of rows from the beginning of the result set. It is often used in combination with the FETCH or LIMIT clause to paginate the results of a query.

The syntax for using the OFFSET clause is as follows:

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ...
OFFSET n ROWS;

```

In the above query, replace column1, column2, ... with the actual column names you want to select from the table, and replace table_name with the name of the table you're querying. The ORDER BY clause specifies the column(s) by which you want to order the result set.

Finally, the OFFSET n ROWS clause specifies the number of rows to skip from the beginning of the result set. Replace n with the desired number of rows to skip.

Here's an example to illustrate its usage:

```sql
SELECT name, age
FROM employees
ORDER BY name
OFFSET 10 ROWS;
```

The above query retrieves the name and age columns from the employees table, orders the result set by the name column, and skips the first 10 rows.

Note that the availability and exact syntax of the OFFSET clause may vary slightly depending on the specific database system you're using.


### Advantages of Offset

1. Pagination: One of the primary use cases for the OFFSET clause is to implement pagination in query results. By specifying an OFFSET value, you can retrieve a specific "page" of results from a larger result set. This is particularly useful when dealing with large datasets or when you want to display results in smaller, manageable chunks.
1. Dynamic Result Sets: The OFFSET clause allows you to dynamically control the number of rows returned in a query result. By adjusting the OFFSET value, you can easily retrieve different subsets of data from a table, enabling you to explore the data in a more granular manner.
2. Sorting and Ranking: When combined with the ORDER BY clause, the OFFSET clause allows you to sort the result set based on specific criteria. This is useful when you want to retrieve rows starting from a certain point in the ordered result set. For example, you can skip the top 'n' rows and retrieve the subsequent rows.
4. Efficient Data Retrieval: With the OFFSET clause, you can efficiently retrieve a specific portion of data without having to fetch the entire result set. This can be especially beneficial when working with large tables or when network bandwidth is a concern.

Despite its advantages, it's important to note that the OFFSET clause can have performance implications, especially when dealing with large OFFSET values. As the OFFSET increases, the database engine needs to skip more rows, potentially leading to slower query execution. In such cases, alternative techniques like keyset pagination or using seek methods may provide better performance.

### Disadvantages of Offset

While the OFFSET clause in SQL provides advantages for pagination and result set manipulation, it also has some disadvantages to consider:

1. Performance Impact: Using the OFFSET clause can have a negative impact on performance, particularly when working with large OFFSET values or large result sets. The database engine needs to skip a certain number of rows before returning the desired result set, which can be computationally expensive. As the OFFSET value increases, the execution time of the query may also increase significantly.
1. Resource Usage: The OFFSET clause requires the database engine to process and retrieve the skipped rows before returning the desired rows. This can consume additional system resources, such as memory and processing power, especially when dealing with large OFFSET values or complex queries.
1. Inefficient for Deep Paging: If you need to access pages deep within a result set, the OFFSET clause becomes less efficient. For example, if you want to retrieve rows from the middle or end of a large result set, the database has to skip a substantial number of rows, potentially leading to slower query execution.
1. Impact on Consistency: The result set returned by a query using the OFFSET clause can be affected by concurrent modifications to the underlying data. If rows are inserted, updated, or deleted between different executions of the same query, the skipped rows may change or new rows may be included, leading to inconsistency in the result set.
1. Limited Support: The availability and syntax of the OFFSET clause can vary across different database systems. Some database systems may not support the OFFSET clause at all or may provide alternative ways to achieve similar functionality. This lack of universal support can make it challenging to write portable SQL code.

To mitigate these disadvantages, it's worth exploring alternative pagination techniques such as keyset pagination, which rely on using unique column values rather than row offsets. These techniques can provide better performance and consistency for retrieving subsets of data from large result sets.

## Life With out Offset

### Keysets

Keyset pagination, also known as keyset cursors or seek methods, is an alternative pagination technique that addresses some of the disadvantages associated with the OFFSET clause. Instead of relying on row offsets, keyset pagination uses unique column values to identify and retrieve specific subsets of data.

```sql
SELECT *
FROM `table`
WHERE id < ?last_seen_id
ORDER BY id DESC
FETCH FIRST 10 ROWS ONLY
```

This approach—called seek method or keyset pagination—solves the problem of drifting results as illustrated above and is even faster than offset. 


### Keyset vs Offset

Offset instructs the databases skip the first N results of a query. However, the database must still fetch these rows from the disk and bring them in order before it can send the following ones.



[Slide](https://www.slideshare.net/MarkusWinand/p2d2-pagination-done-the-postgresql-way)
[No Offset](http://use-the-index-luke.com/no-offset)
