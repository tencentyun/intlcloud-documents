This document describes the SQL usage specifications and suggestions after a TDSQL-C for MySQL cluster is created.

## Basic database design specifications
- All characters are stored and represented in UTF-8 or utf8mb4 encoding. Tables and fields must have comments.
- Avoid using large transactions.
>?For example, if you run multiple SELECT or UPDATE statements in a frequently executed transaction, the concurrency capabilities of MySQL will be compromised severely, as the resources such as locks held by the transaction can be released only when the transaction is rolled back or committed. In addition, the consistency of data writes also needs to be assessed.

## Database SQL query specifications
- When using ORDER BY ... LIMIT queries, consider optimizing the query statements through index to improve the efficiency.
- Keep the number of rows in the result set filtered by a WHERE condition in ORDER BY, GROUP BY, and DISTINCT queries below 1,000; otherwise, the query will be inefficient.
- Use an index to directly retrieve the sorted data for ORDER BY, GROUP BY, and DISTINCT statements. For example, you can use `key(a,b)` for `where a=1 order by b`.
- When using JOIN queries, use indexes in the same table in the WHERE condition as much as possible.
>?For example, in the statement `select t1.a, t2.b from t1,t2 where t1.a=t2.a and t1.b=123 and t2.c= 4`:
If the `t1.c` and `t2.c` fields have the same value, only `b` in the index `(b,c)` in `t1` is used. If you change `t2.c=4` in the WHERE condition to `t1.c=4`, you can use the complete index. Such cases may occur in field redundancy design (denormalization).
- We recommend you use UNION ALL to reduce the use of UNION. You need to consider whether to deduplicate the data.
As UNION ALL doesn't deduplicate and sort the data, it runs faster than UNION. If your business doesn't need deduplication, use UNION ALL preferentially.
- When you implement the paginated query logic in your code, the result should be returned directly if COUNT is 0. This avoids executing subsequent pagination statements.
- Avoid frequently performing the COUNT operation on tables, as it takes a long time (generally seconds) on big tables. If you need to frequently perform COUNT, use a dedicated counter table.
- If you are sure that there is only one returned result, use `LIMIT 1`. If you can determine the number of results provided that the data is correct, use LIMIT queries as much as possible to return results more quickly.
- You can change the DELETE and UPDATE statements to SELECT and perform EXPLAIN to evaluate their performance. Too many SELECT statements will slow down the database and may even lock a table, which will restrict writes to the table.
- TRUNCATE TABLE runs faster and uses fewer system and log resources than DELETE. It is recommended if you need to delete an entire table with no triggers.
>?
>- TRUNCATE TABLE doesn't write the deleted data to the log file.
>- TRUNCATE TABLE acts the same as DELETE with no WHERE clauses.
>- TRUNCATE TABLE cannot be written in the same transaction as other DML statements.
- Avoid using negative queries and scanning full tables.
>?A negative query refers to a query using negative operators such as NOT, !=, <>, NOT EXISTS, NOT IN, and NOT LIKE. Negative queries cannot perform binary searches by using the index structure but can only scan full tables.
- Avoid use JOIN to join more than three tables. The fields to be joined must have the same data type.
- In multi-table join queries, make sure that joined fields have an index. Select the table with the smallest result set as the driving table to join other tables in a multi-table join. You need to keep an eye on the table index and SQL performance even for dual-table join.

## Database SQL development specifications
- Consider splitting simple SQL statements.
>?For example, in the OR condition `f_phone='10000' or f_mobile='10000'`, the two fields have their respective index, but only one will be used. In this case, you can split it into two SQL statements or use UNION ALL.
- If you need to implement complex computing or business logic in SQL, consider implementing it at the business layer.
- Use an appropriate pagination method to improve the pagination efficiency. Do not use skip paging for large pages.
>?
>- For example, if the pagination statement is as follows:
>`SELECT * FROM table1 ORDER BY ftime DESC LIMIT 10000,10;`
>A high number of I/O operations will be generated, as MySQL uses the read-ahead policy.
>- We recommend you pass in the limit value of the last pagination for the current pagination.
>`SELECT * FROM table1 WHERE ftime < last_time ORDER BY ftime DESC LIMIT 10;`
- Write update statements based on the primary key or unique key in transactions; otherwise, gap locks will be generated, and the lock scope will be expanded internally, which will compromise the system performance and generate deadlocks.
- Do not use foreign keys and cascading. Implement the foreign key logic at the application layer.
>?For example, as `student_id` is the primary key in the student table, it is a foreign key in the score table. If the update of `student_id` in the student table triggers the update of `student_id` in the score table, then it is a cascading update.
>Foreign keys and cascading updates are suitable for a standalone instance with a low concurrency but not a distributed cluster with a high concurrency.
>Cascading updates have risks of database update storms, and foreign keys slow down insertions into the database.
- Reduce IN operations. Keep the number of elements in the set after IN below 500.
- Appropriately use batch SQL statements like `INSERT INTO … VALUES (XX),(XX),(XX)....(XX);` to reduce interactions with the database. Here, we recommend you keep the number of `XX` items below 100.
- Avoid using procedures, as they are hard to debug and extend and have no portability.
- Avoid using triggers, event schedulers, and views to implement the business logic, which should be processed at the business layer to prevent logic dependency on the database.
- Avoid using implicit type conversion.
>?Below are the specific conversion rules:
>1. When at least one parameter between the two is NULL, the comparison result will also be NULL. A special case is that when `<=>` is used to compare two NULL values, `1` will be returned. However, in both cases, such type conversion is not needed.
>2. If both parameters are strings, they will be compared as strings without type conversion.
>3. If both parameters are integers, they will be compared as integers without type conversion.
>4. When a hexadecimal value is compared with a non-numeric value, it will be treated as a binary string.
>5. If a parameter is of TIMESTAMP or DATETIME type, and the other is a constant, the constant will be converted into a TIMESTAMP value.
>6. If a parameter is a decimal, and the other is an integer, the integer will be converted into a decimal for comparison. If the other parameter is a floating-point number, the decimal will be converted into a floating-point number for comparison.
>7. In other cases, both parameters will be converted into floating-point numbers for comparison.
>8. If an index is created for a string field, and the field is compared with an INT value, rule 7 will apply.
If the type defined by `f_phone` is VARCHAR but `f_phone in (098890)` is used in the WHERE clause, both parameters will be converted into FLOAT values. In this case, FLOAT values converted from strings will make MySQL unable to use indexes and compromise the performance.
If `f_user_id ='1234567'` is used, rule 2 will apply, and the number will be directly treated as a string for comparison.
- Use as few SQL statements in a transaction as possible if the business permits. Keep the number of statements below 5, as a long transaction will cause problems such as long data lock, internal MySQL cache, and excessive connection consumption.
- Avoid using natural joins.
>?Natural joins don't display or define the joined columns but imply them, so they may be hard to understand or cannot be ported.

## Database index design specifications
- Reduce the use of ORDER BY query statements that cannot be optimized through an index based on the actual business needs, as ORDER BY consumes a lot of CPU resources.
- If complex SQL statements are involved, design them by referring to existing indexes, execute EXPLAIN to view execution plans, and use indexes to add more query restrictions.
- When using a new SELECT, UPDATE, or DELETE statement, you need to use EXPLAIN to view the index usage in the execution plan. Try preventing the `Extra` column from displaying `Using File Sort` and `Using Temporary`. If the number of rows scanned in the execution plan exceeds 1,000, assess whether to allow launching the code. You also need to collect and analyze the statistics of slow logs daily to handle slow log statements promptly.
>?Notes on EXPLAIN:
>- types: ALL, index, range, ref, eq_ref, const, system, NULL (the farther to the left, the higher the performance).
>- possible_keys: It refers to which index can be used by MySQL to find the record in the table. If a field involved in the query has an index, the index will be listed but won't necessarily be used for query.
>- key: It indicates the key (index) that MySQL actually decides to use. If no indexes are selected, the key will be NULL. To force MySQL to use or ignore indexes in the `possible_keys` column, use `FORCE INDEX`, `USE INDEX`, or `IGNORE INDEX` in the query.
>- ref: It indicates which columns or variables are used to query the values in the index column.
>- rows: It indicates the number of rows to be read to find the required records estimated based on the table statistics and index usage.
>- Extra:
   - Using temporary: It indicates that MySQL needs to use a temp table to store the result set, which is often seen in sorting and paginated queries.
   - Using filesort: Filesort refers to a sorting operation that cannot be completed by using an index in MySQL.
   - Using index: It indicates that an index is used. If only `Using index` is displayed, no data tables are queried, and only an index table is used to complete the query. This is called covering index. If `Using where` is also displayed, an index is also used to search for and read the records, in which case data tables need to be queried.
   - Using where: It indicates a conditional query. If the entire table is not read, or not all required data can be obtained through indexes, `Using where` will be displayed. If the `type` column is `ALL` or `index`, and this prompt is not displayed, you may be executing an incorrect query, and all data will be returned.
- If a function is used in the WHERE condition column, indexes will become invalid.
>?For example, in `WHERE left(name, 5) = 'zhang'`, the `left` function will invalidate the indexes for `name`. You can modify the condition in your business to stop using the function. If the returned result set is small, you can also filter eligible rows in your business.

