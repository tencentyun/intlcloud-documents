This document describes the usage specifications and suggestions after a TDSQL-C for MySQL cluster is created.

## Database permission specifications
- All DDL operations (such as creating tables and modifying table structures) can only be performed by DBAs through Database Management Center (DMC) during off-peak hours after approval.
- Permissions should be managed in a fine-grained manner by separating read, write, Ops, and development permissions.
- DDL operations logs should be retained.

## Database and table specifications
- All created MySQL tables must use the InnoDB engine; otherwise, transactions are not supported.
- The decimal type must be DECIMAL. FLOAT or DOUBLE cannot be used.
>?FLOAT and DOUBLE values may lose their precision and cause rounding errors when stored. If a value to be stored is out of the range of DECIMAL, split the value into INTEGER and DECIMAL parts and store them separately.
- The following reserved words cannot be used: DESC, RANGE, MATCH, and DELAYED. For more information, see [Keywords and Reserved Words](https://dev.mysql.com/doc/refman/8.0/en/keywords.html).
- A data table must use a business-relevant ordered unique field or a business-irrelevant auto-increment field as the primary key.
>?The lack of the primary key can easily cause slow source database execution and replication delay.
- A table field must have a default value and cannot be NULL. If the field is of numeric type, we recommend you use `0` as its default value. If the field is of a character type such as VARCHAR, we recommend you use an empty string ''.
- We recommend you make each table contain two DATETIME fields: `create_time` and `update_time`.
>?You can get the required data from a data warehouse based on these two fields without consulting the business team.
>When an exception occurs in the database, you can use these two fields to determine the time when the data is inserted and updated or determine whether to restore data in extreme cases.
- Keep the number of fields in a single table below 50.
- If the lengths of stored strings are almost the same, use fixed-length CHAR strings.
- Provided that the data consistency is ensured, cross-table redundant fields are allowed to avoid correlated subqueries and improve the query performance.
>?Redundant fields must comply with the following rules:
>- The fields are not frequently modified.
>- The fields are not large VARCHAR or TEXT.
- Data types with a proper storage length can accelerate search while saving the database tablespace and index storage space. LONG TEXT and BLOB are not recommended.

## Index specifications
- Use the same field type to prevent implicit conversion from causing invalid indexes.
- We recommend you create a unique index for all minimum sets of fields with uniqueness in your business, even if they are field combinations.
For example, if a table contains fields `a`, `b`, `c`, `d`, `e`, and `f`, and field combinations `ab` and `ef` have uniqueness, then we recommend you create unique indexes for `ab` and `ef` respectively.
>?
>- Even if complete verification control is implemented at the application layer, dirty data may be generated as long as there is no unique index.
>- Before creating a unique index, consider whether it is indeed helpful to the query. Useless indexes can be deleted.
>- Assess the impact of extra indexes on the INSERT operation performance. Determine whether to create unique indexes based on the requirements for the correctness and performance of data with uniqueness.
- Create indexes on fixed-length fields such as INT fields. When creating an index on a VARCHAR field, you must specify the index length, but you don't need to create an index on the entire field; instead, determine the index length based on the actual text distinction.
>?The index length and distinction are a pair of contradictions. Generally, for strings, the distinction of an index with a length of 20 bytes will be higher than 90%. The distinction formula is `count(distinct left(column name, index length))/count(*)`. Place the column names with a high distinction on the left.
- If possible, do not use left fuzzy searches (such as `SELECT * FROM users WHERE u_name LIKE '%hk'`) or full fuzzy searches on pages; otherwise, index scan may downgrade to full-table scan.
>?An index file has the leftmost prefix match feature of B-tree. If the value on the left is not determined, the index cannot be used.
- Use a covering index to query data and avoid returning to the table. However, do not add too many fields to the covering index; otherwise, the write performance will be compromised.
>?Types of indexes that can be created include primary key, unique, and normal indexes. A covering index indicates that if you execute an EXPLAIN statement for query, `using index` will be displayed in the `Extra` column.
- Optimize the SQL performance as follows: `range` (minimum level), `ref` (basic level), and `consts` (maximum level).
- When creating a composite index, place the column with the highest distinction on the left.
- Keep the number of indexes in a single table below 5 or 20% of the number of table fields.
- Avoid the following misunderstandings when creating indexes:
 - Indexes should be frequently used. An index needs to be created for a query.
 - Indexes should be as few as possible. Indexes takes up the space and slow down updates and insertions.
 - Unique indexes are not needed. Business uniqueness must be implemented at the application layer in the "query first and then insert" method.
