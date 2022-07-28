It retrieves rows from a table or view.

## Synopsis
```
[ WITH with_query [, ...] ]
SELECT [ALL | DISTINCT [ON (expression [, ...])]]
  * | expression [[AS] output_name] [, ...]
  [FROM from_item [, ...]]
  [WHERE condition]
  [GROUP BY grouping_element [, ...]]
  [HAVING condition [, ...]]
  [WINDOW window_name AS (window_specification)]
  [{UNION | INTERSECT | EXCEPT} [ALL] select]
  [ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]]
  [LIMIT {count | ALL}]
  [OFFSET start]
  [FOR {UPDATE | SHARE} [OF table_name [, ...]] [NOWAIT] [...]]
```
where `with_query` is:
```
with_query_name [( column_name [, ...] )] AS ( select )
```
where `grouping_element` can be one of:
```
()
expression
ROLLUP (expression [,...])
CUBE (expression [,...])
GROUPING SETS ((grouping_element [, ...]))
```
where `window_specification` can be:
```
  [window_name]
  [PARTITION BY expression [, ...]]
  [ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]
     [{RANGE | ROWS} 
          { UNBOUNDED PRECEDING
          | expression PRECEDING
          | CURRENT ROW
          | BETWEEN window_frame_bound AND window_frame_bound }]]
```
where `window_frame_bound` can be one of:
```
UNBOUNDED PRECEDING
expression PRECEDING
CURRENT ROW
expression FOLLOWING
UNBOUNDED FOLLOWING
```
where `from_item` can be one of:
```
[ONLY] table_name [[AS] alias [( column_alias [, ...] )]]
(select) [AS] alias [( column_alias [, ...] )]
with_query_name [ [AS] alias [( column_alias [, ...] )]]
function_name ( [argument [, ...]] ) [AS] alias
             [( column_alias [, ...] 
                | column_definition [, ...] )]
function_name ( [argument [, ...]] ) AS 
              ( column_definition [, ...] )
from_item [NATURAL] join_type from_item
          [ON join_condition | USING ( join_column [, ...] )]
```

## Description
`SELECT` retrieves rows from zero or more tables. The general processing of `SELECT` is as follows:
 - All queries in the `WITH` list are computed. These effectively serve as temporary tables that can be referenced in the `FROM` list.
 - All elements in the `FROM` list are computed. (Each element in the `FROM` list is a real or virtual table.) If more than one element is specified in the `FROM` list, they are cross-joined together.
 - If the `WHERE` clause is specified, all rows that do not satisfy the condition are eliminated from the output.
 - If the `GROUP BY` clause is specified, or if there are aggregate function calls, the output is combined into groups of rows that match on one or more values, and the results of aggregate functions are computed. If the `HAVING` clause is present, it eliminates groups that do not satisfy the given condition.
 - If a `WINDOW` expression (optional `WINDOW` clause) is specified, the output is organized by window frame based on position (row) or value (range).
 - `DISTINCT` eliminates duplicate rows from the result. `DISTINCT ON` eliminates rows that match on all the specified expressions. `ALL` (the default) will return all candidate rows, including duplicates.
 - The actual output rows are computed using the `SELECT` output expressions for each selected row.
 - Using the operators `UNION`, `INTERSECT`, and `EXCEPT`, the output of more than one SELECT statement can be combined to form a single result set.
   - The `UNION` operator returns all rows that are in one or both of the result sets.
   - The `INTERSECT` operator returns all rows that are strictly in both result sets.
   - The `EXCEPT` operator returns the rows that are in the first result set but not in the second.
   In all three cases, duplicate rows are eliminated unless `ALL` is specified.
 - If the `ORDER BY` clause is specified, the returned rows are sorted in the specified order. If `ORDER BY` is not given, the rows are returned in whatever order the system finds fastest to produce.
 - If the `LIMIT` or `OFFSET` clause is specified, the `SELECT` statement only returns a subset of the result rows.
 - If `FOR UPDATE` or `FOR SHARE` is specified, the `SELECT` statement locks the selected rows against concurrent updates.
You must have `SELECT` privilege on the table from where to read values. The use of `FOR UPDATE` and `FOR SHARE` requires `UPDATE` privilege as well

## Parameters
### **WITH clause**
The `WITH` clause allows you to specify one or more subqueries that can be referenced by name in the primary query. The subqueries effectively act as temporary tables or views for the duration of the primary query. Each subquery can be a `SELECT` or `VALUES` statement.

A name (without schema qualification) must be specified for each `WITH` query. Optionally, a list of column names can be specified; if this is omitted, the column names are inferred from the subquery. The primary query and all `WITH` queries are (theoretically) executed at the same time.

**SELECT list**
The `SELECT` list (between the keywords `SELECT` and `FROM`) specifies expressions that form the output rows of the `SELECT` statement. The expressions can (and usually do) refer to columns computed in the `FROM` clause.

To specify the name to use for an output column, write `[AS] output_name`. This name is just used to label the column for display. An output column's name can be used to refer to the column's value in `ORDER BY` and `GROUP BY` clauses, but not in the `WHERE` or `HAVING` clauses; there you must write out the expression instead.

The `AS` keyword is optional in most cases (for example, when declaring an alias for a column name, constant, function call, or simple unary operation expression). To prevent any possible conflict between declared aliases and keywords, the output name must be double-quoted. It is recommended that you always either write `AS` or double-quote the output name.

An expression in the `SELECT` list can be a constant value, a column reference, an operator invocation, a function call, a window expression, a scalar subquery, and so on.


### **FROM clause**
The `FROM` clause specifies one or more source tables for the `SELECT`. If multiple sources are specified, the result is the Cartesian product (cross join) of all the sources. But usually qualification conditions are added to restrict the returned rows to a small subset of the Cartesian product. The `FROM` clause can contain the following elements:
- table_name
The name (optionally schema-qualified) of an existing table or view. If `ONLY` is specified before the table name, only that table is scanned. If `ONLY` is not specified, the table and all its descendant tables (if any) are scanned.
- alias
A substitute name for the `FROM` item containing the alias. An alias is used for brevity or to eliminate ambiguity for self-joins (where the same table is scanned multiple times). When an alias is provided, it completely hides the actual name of the table or function; for example given `FROM foo AS f`, the remainder of the `SELECT` must refer to this `FROM` item as `f` not `foo`. If an alias is written, a column alias list can also be written to provide substitute names for one or more columns of the table.
- select
A sub-`SELECT` can appear in the `FROM` clause. This acts as though its output were created as a temporary table for the duration of this single `SELECT` command. **Note that the sub-`SELECT` must be surrounded by parentheses, and an alias must be provided for it. A `VALUES` command can also be used here.**
- with_query_name
A `WITH` query is referenced in the `FROM` clause by specifying its `WITH` query name, just as though the name were a table name. The `WITH` query name cannot contain a schema qualifier. An alias can be provided in the same way as for a table.
- function_name
Function calls can appear in the `FROM` clause. (This is especially useful for functions that return result sets, but any function can be used.) This acts as though its output were created as a temporary table for the duration of this single `SELECT` command. An alias may also be used.
If an alias is written, a column alias list can also be written to provide substitute names for one or more attributes of the function's composite return type. If the function has been defined as returning the `record` data type, then an alias or the keyword `AS` must be present, followed by a column definition list in the form ( column_name data_type [, ... ] ). The column definition list must match the actual number and types of columns returned by the function.
- join_type
One of:
 - **[INNER] JOIN**
 - **LEFT [OUTER] JOIN**
 - **RIGHT [OUTER] JOIN**
 - **FULL [OUTER] JOIN**
 - **CROSS JOIN**

For the `INNER` and `OUTER` join types, a join condition must be specified, namely exactly one of `NATURALON join_condition` or `USING ( join_column [, ...])`. See below for the meaning. For CROSS JOIN, none of these clauses may appear.

A `JOIN` clause combines two result tables. Use parentheses if necessary to determine the order of nesting. In the absence of parentheses, `JOINs` nest left-to-right. In any case `JOIN` binds more tightly than the commas separating `JOIN`-list items.

`CROSS JOIN` and `INNER JOIN` produce a simple Cartesian product, the same result as you get from listing the two tables at the top level of `FROM`, but restricted by the join condition (if any). `CROSS JOIN` is equivalent to `INNER JOIN ON(TRUE)`, that is, no rows are removed by qualification. These join types are just a notational convenience, since they do nothing you could not do with plain `FROM` and `WHERE`.

`LEFT OUTER JOIN` returns all rows in the qualified Cartesian product (i.e., all combined rows that pass its join condition), plus one copy of each row in the left-hand table for which there was no right-hand row that passed the join condition. This left-hand row is extended to the full width of the joined table by inserting null values for the right-hand columns. Note that only the `JOIN` clause's own condition is considered while deciding which rows have matches.

Conversely, `RIGHT OUTER JOIN` returns all the joined rows, plus one row for each unmatched right-hand row (extended with nulls on the left). This is just a notational convenience, since you could convert it to a `LEFT OUTER JOIN` by switching the left and right tables.

`FULL OUTER JOIN` returns all the joined rows, plus one row for each unmatched left-hand row (extended with nulls on the right), plus one row for each unmatched right-hand row (extended with nulls on the left).

**ON join_condition**
`join_condition` is an expression resulting in a value of type boolean (similar to a `WHERE` clause) that specifies which rows in a join are considered to match.

USING (join_column [, ...])
A clause of the form `USING ( a, b, ... )` is shorthand for `ON left_table.a = right_table.a AND left_table.b = right_table.b ...`. Also, `USING` implies that only one of each pair of equivalent columns will be included in the join output, not both.

**NATURAL**
`NATURAL` is shorthand for a `USING` list that mentions all columns in the two tables that have the same names.

### **WHERE clause**
The optional `WHERE` clause has the general form:
```sql
WHERE condition
```
where `condition` is any expression that evaluates to a result of type boolean. Any row that does not satisfy this condition will be eliminated from the output. A row satisfies the condition if it returns true when the actual row values are substituted for any variable references.

### **GROUP BY clause**
The optional `GROUP BY` clause has the general form:
```sql
GROUP BY grouping_element [, ...]
```
where `grouping_element` can be one of:
```sql
()
expression
ROLLUP (expression [,...])
CUBE (expression [,...])
GROUPING SETS ((grouping_element [, ...]))
```
`GROUP BY` will condense into a single row all selected rows that share the same values for the grouped expressions. `expression` can be an input column name, or the name or ordinal number of an output column (`SELECT` list item), or an arbitrary expression formed from input-column values. In case of ambiguity, a `GROUP BY` name will be interpreted as an input column name rather than an output column name.

Aggregate functions, if any are used, are computed across all rows making up each group, producing a separate value for each group. (If there are aggregate functions but no `GROUP BY` clause, the query is treated as having a single group comprising all the selected rows.) When `GROUP BY` is present, or any aggregate functions are present, it is not valid for the `SELECT` list expressions to refer to ungrouped columns except within aggregate functions or when the ungrouped column is functionally dependent on the grouped columns, since there would otherwise be more than one possible value to return for an ungrouped column.

The database has the following additional OLAG grouping extensions (often referred to as `supergroups`):
- ROLLUP
A `ROLLUP` grouping is an extension to the `GROUP BY` clause that creates aggregate subtotals that roll up from the most detailed level to a grand total, following a list of grouping columns (or expressions). `ROLLUP` takes an ordered list of grouping columns, calculates the standard aggregate values specified in the `GROUP BY` clause, then creates progressively higher-level subtotals, moving from right to left through the list. Finally, it creates a grand total. A `ROLLUP` grouping can be thought of as a series of grouping sets. For example:
```sql
GROUP BY ROLLUP (a,b,c) 
```
 is equivalent to:
```sql
GROUP BY GROUPING SETS( (a,b,c), (a,b), (a), () ) 
```
 Notice that the n elements of a `ROLLUP` translate to n+1 grouping sets. Also, the order in which the grouping expressions are specified is significant in a `ROLLUP`.
- CUBE
A `CUBE` grouping is an extension to the `GROUP BY` clause that creates subtotals for all of the possible combinations of the given list of grouping columns (or expressions). In terms of multidimensional analysis, `CUBE` generates all the subtotals that could be calculated for a data cube with the specified dimensions. For example:
```sql
GROUP BY CUBE (a,b,c) 
```
 is equivalent to:
```sql
GROUP BY GROUPING SETS( (a,b,c), (a,b), (a,c), (b,c), (a), 
(b), (c), () ) 
```
 Notice that n elements of a `CUBE` translate to 2n grouping sets. Consider using `CUBE` in any situation requiring cross-tabular reports. `CUBE` is typically most suitable in queries that use columns from multiple dimensions rather than columns representing different levels of a single dimension. For instance, a commonly requested cross-tabulation might need subtotals for all the combinations of month, state, and product.
- GROUPING SETS
You can selectively specify the set of groups that you want to create using a `GROUPING SETS` expression within a `GROUP BY` clause. This allows precise specification across multiple dimensions without computing a whole `ROLLUP` or `CUBE`. For example:
```sql
GROUP BY GROUPING SETS( (a,c), (a,b) )
```
 If using the grouping extension clauses `ROLLUP`, `CUBE`, or `GROUPING SETS`, two challenges arise. First, how do you determine which result rows are subtotals, and then the exact level of aggregation for a given subtotal. Or, how do you differentiate between result rows that contain both stored `NULL` values and "NULL" values created by the `ROLLUP` or `CUBE`. Secondly, when duplicate grouping sets are specified in the `GROUP BY` clause, how do you determine which result rows are duplicates? There are two additional grouping functions you can use in the `SELECT` list to help with this:
 - **grouping(column      [, ...])**: The `grouping` function can be applied to one or more grouping attributes to distinguish super-aggregated rows from regular grouped rows. This can be helpful in distinguishing a "NULL" representing the set of all values in a super-aggregated row from a `NULL` value in a regular row. Each argument in this function produces a bit — either 1 or 0, where 1 means the result row is super-aggregated, and 0 means the result row is from a regular grouping.
The `grouping` function returns an integer by treating these bits as a binary number and then converting it to a base-10 integer.
 - **group_id()**: For grouping extension queries that contain duplicate grouping sets, the `group_id` function is used to identify duplicate rows in the output. All `*unique*` grouping set output rows will have a `group_id` value of 0. For each duplicate grouping set detected, the `group_id` function assigns a `group_id` number greater than 0.
All output rows in a particular duplicate grouping set are identified by the same `group_id` number.

### **WINDOW clause**
The `WINDOW` clause is used to define a window that can be used in the `OVER()` expression of a window function (such as `rank` or `avg`). For example:
```sql
SELECT vendor, rank() OVER (mywindow) FROM sale
GROUP BY vendor
WINDOW mywindow AS (ORDER BY sum(prc*qty));
```
 A `WINDOW` clause has this general form:
```sql
WINDOW window_name AS (window_specification)
```
 where `window_specification` can be:
```sql
[window_name]
[PARTITION BY expression [, ...]]
[ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]
    [{RANGE | ROWS} 
      { UNBOUNDED PRECEDING
      | expression PRECEDING
      | CURRENT ROW
      | BETWEEN window_frame_bound AND window_frame_bound }]]
             where `window_frame_bound` can be one of:
               UNBOUNDED PRECEDING
               expression PRECEDING
               CURRENT ROW
               expression FOLLOWING
               UNBOUNDED FOLLOWING
```
 window_name
Gives a name to the window specification.

PARTITION BY
The `PARTITION BY` clause organizes the result set into logical groups based on the unique values of the specified expression. When used with window functions, the functions are applied to each partition independently. For example, if you follow `PARTITION BY` with a column name, the result set is partitioned by the distinct values of that column. If omitted, the entire result set is considered one partition.

ORDER BY
The `ORDER BY` clause defines how to sort the rows in each partition of the result set. If omitted, rows are returned in whatever order is most efficient and may vary. 
>?Columns of data types that lack a coherent ordering, such as `time`, are not good candidates for use in the `ORDER BY` clause of a window specification. Time, with or without time zone, lacks a coherent ordering because addition and subtraction do not have the expected effects. For example, the following is not generally true: `x::time < x::time + '2 hour'::interval`.

ROWS | RANGE
Use either a `ROWS` or `RANGE` clause to express the bounds of the window. The window bound can be one, many, or all rows of a partition. You can express the bound of the window either in terms of a range of data values offset from the value in the current row (`RANGE`), or in terms of the number of rows offset from the current row (`ROWS`).

When using the `RANGE` clause, you must also use an `ORDER BY` clause. This is because the calculation performed to produce the window requires that the values be sorted. Additionally, the `ORDER BY` clause cannot contain more than one expression, and the expression must result in either a date or a numeric value. When using the `ROWS` or `RANGE` clauses, if you specify only a starting row, the current row is used as the last row in the window.

**PRECEDING**: The `PRECEDING` clause defines the first row of the window using the current row as a reference point. The starting row is expressed in terms of the number of rows preceding the current row. For example, in the case of `ROWS` framing, `5 PRECEDING` sets the window to start with the fifth row preceding the current row. In the case of `RANGE` framing, it sets the window to start with the first row whose ordering column value precedes that of the current row by 5 in the given order. If the specified order is ascending by date, this will be the first row within five days before the current row. `UNBOUNDED PRECEDING` sets the first row in the window to be the first row in the partition.

**BETWEEN**: The `BETWEEN` clause defines the first and last row of the window, using the current row as a reference point. First and last rows are expressed in terms of the number of rows preceding and following the current row, respectively. For example, `BETWEEN 3 PRECEDING AND 5 FOLLOWING` sets the window to start with the third row preceding the current row, and end with the fifth row following the current row. Use `BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING` to set the first and last rows in the window to be the first and last row in the partition, respectively. This is equivalent to the default behavior if no `ROW` or `RANGE` clause is specified.

**FOLLOWING**: The `FOLLOWING` clause defines the last row of the window using the current row as a reference point. The last row is expressed in terms of the number of rows following the current row. For example, in the case of `ROWS` framing, `5 FOLLOWING` sets the window to end with the fifth row following the current row. In the case of `RANGE` framing, it sets the window to end with the last row whose ordering column value follows that of the current row by 5 in the given order. If the specified order is ascending by date, this will be the last row within five days after the current row. Use `UNBOUNDED FOLLOWING` to set the last row in the window to be the last row in the partition.

If you do not specify a `ROW` or a `RANGE` clause, the window bound starts with the first row in the partition (`UNBOUNDED PRECEDING`) and ends with the current row (`CURRENT ROW`) if `ORDER BY` is used. If an `ORDER BY` is not specified, the window starts with the first row in the partition (`UNBOUNDED PRECEDING`) and ends with last row in the partition (`UNBOUNDED FOLLOWING`).

### **HAVING clause**
The optional `HAVING` clause has the general form:
```sql
HAVING condition
```
where `condition` is the same as specified for the `WHERE` clause. `HAVING` eliminates group rows that do not satisfy the condition.
`HAVING` is different from `WHERE`: `WHERE` filters individual rows before the application of `GROUP BY`, while `HAVING` filters group rows created by `GROUP BY`. Each column referenced in `condition` must unambiguously reference a grouping column, unless the reference appears within an aggregate function.

The presence of `HAVING` turns a query into a grouped query even if there is no `GROUP BY` clause. This is the same as what happens when the query contains aggregate functions but no `GROUP BY` clause. All the selected rows are considered to form a single group, and the `SELECT` list and `HAVING` clause can only reference table columns from within aggregate functions. Such a query will emit a single row if the `HAVING` condition is true, zero rows if it is not true.

### **UNION clause**
The `UNION` clause has this general form:
```sql
select_statement UNION [ALL] select_statement
```
where `select_statement` is any `SELECT` statement without an `ORDER BY`, `LIMIT`, `FOR UPDATE`, `FOR SHARE`, or `FOR KEY SHARE` clause. (`ORDER BY` and `LIMIT` can be attached to a subquery expression if it is enclosed in parentheses. Without parentheses, these clauses will be taken to apply to the result of the `UNION`, not to its right-hand input expression.)

The `UNION` operator computes the set union of the rows returned by the involved `SELECT` statements. A row is in the set union of two result sets if it appears in at least one of the result sets. The two `SELECT` statements that represent the direct operands of the `UNION` must produce the same number of columns, and corresponding columns must be of compatible data types.

The result of `UNION` does not contain any duplicate rows unless the `ALL` option is specified. `ALL` prevents elimination of duplicates. (Therefore, `UNION ALL` is usually significantly quicker than `UNION`; use `ALL` when you can.)

Multiple `UNION` operators in the same `SELECT` statement are evaluated left to right, unless otherwise indicated by parentheses.

Currently, `FOR UPDATE` and `FOR SHARE` may not be specified either for a `UNION` result or for any input of a `UNION`.

### **INTERSECT** **clause**
The `INTERSECT` clause has this general form:
```sql
select_statement INTERSECT [ALL] select_statement
```
where `select_statement` is any `SELECT` statement without an `ORDER BY`, `LIMIT`, `FOR UPDATE`, or `FOR SHARE` clause.

The `INTERSECT` operator computes the set intersection of the rows returned by the involved `SELECT` statements. A row is in the intersection of two result sets if it appears in both result sets.

The result of `INTERSECT` does not contain any duplicate rows unless the `ALL` option is specified. With `ALL`, a row that has m duplicates in the left table and n duplicates in the right table will appear `min(m, n)` times in the result set.

Multiple `INTERSECT` operators in the same `SELECT` statement are evaluated left to right, unless parentheses dictate otherwise. `INTERSECT` binds more tightly than `UNION`. That is, `A UNION B INTERSECT C` will be read as `A UNION (B INTERSECT C)`.

Currently, `FOR UPDATE` and `FOR SHARE` may not be specified either for an `INTERSECT` result or for any input of an `INTERSECT`.

### **EXCEPT clause**

The `EXCEPT` clause has this general form:
```sql
select_statement EXCEPT [ALL] select_statement
```
where `select_statement` is any `SELECT` statement without an `ORDER BY`, `LIMIT`, `FOR UPDATE`, or `FOR SHARE` clause.

The `EXCEPT` operator computes the set of rows that are in the result of the left `SELECT` statement but not in the result of the right one.

The result of `EXCEPT` does not contain any duplicate rows unless the `ALL` option is specified. With `ALL`, a row that has m duplicates in the left table and n duplicates in the right table will appear `max(m-n,0)` times in the result set.

Multiple `EXCEPT` operators in the same `SELECT` statement are evaluated left to right, unless parentheses dictate otherwise. `EXCEPT` binds at the same level as `UNION`.

Currently, `FOR UPDATE` and `FOR SHARE` may not be specified either for an `EXCEPT` result or for any input of an `EXCEPT`.

### **ORDER BY clause**

The optional `ORDER BY` clause has this general form:
```sql
ORDER BY expression [ASC | DESC | USING operator] [NULLS { FIRST | LAST}] [, ...]
```
where `expression` can be the name or ordinal number of an output column (`SELECT` list item), or it can be an arbitrary expression formed from input column values.

The `ORDER BY` clause causes the result rows to be sorted according to the specified expressions. If two rows are equal according to the left-most expression, they are compared according to the next expression and so on. If they are equal according to all specified expressions, they are returned in an implementation-dependent order.

The ordinal number refers to the ordinal (left-to-right) position of the result column. This feature makes it possible to define an ordering on the basis of a column that does not have a unique name. This is never absolutely necessary because it is always possible to assign a name to a result column using the `AS` clause.

It is also possible to use arbitrary expressions in the `ORDER BY` clause, including columns that do not appear in the `SELECT` result list. Thus the following statement is valid:

```sql
SELECT name FROM distributors ORDER BY code;
```

A limitation of this feature is that an `ORDER BY` clause applying to the result of a `UNION`, `INTERSECT`, or `EXCEPT` clause may only specify an output column name or number, not an expression.

If an `ORDER BY` expression is a simple name that matches both a result column name and an input column name, `ORDER BY` will interpret it as the result column name. This is the opposite of the choice that `GROUP BY` will make in the same situation. This inconsistency is made to be compatible with the SQL standard.

Optionally one may add the keyword `ASC` (ascending) or `DESC` (descending) after any expression in the `ORDER BY` clause. If not specified, `ASC` is assumed by default. Alternatively, a specific ordering operator name may be specified in the `USING` clause. `ASC` is usually equivalent to `USING <` and `DESC` is usually equivalent to `USING >`. (But the creator of a user-defined data type can define exactly what the default sort ordering is, and it might correspond to operators with other names.)

If `NULLS LAST` is specified, null values sort after all non-null values; if `NULLS FIRST` is specified, null values sort before all non-null values. If neither is specified, the default behavior is `NULLS LAST` when `ASC` is specified or implied, and `NULLS FIRST` when `DESC` is specified (thus, the default is to act as though nulls are larger than non-nulls). When `USING` is specified, the default nulls ordering depends upon whether the operator is a less-than or greater-than operator.

Note that ordering options apply only to the expression they follow; for example `ORDER BY x, y DESC` does not mean the same thing as `ORDER BY x DESC, y DESC`.

Character-string data is sorted according to the locale-specific collation order that was established when the database system was initialized.

### DISTINCT clause

If `DISTINCT` is specified, all duplicate rows are removed from the result set (one row is kept from each group of duplicates). `ALL` specifies the opposite: all rows are kept. `ALL` is the default.

`DISTINCT ON ( expression [, ...] )` keeps only the first row of each set of rows where the given expressions evaluate to equal. The `DISTINCT ON` expressions are interpreted using the same rules as for `ORDER BY`. Note that the "first row" of each set is unpredictable unless `ORDER BY` is used to ensure that the desired row appears first. For example:
```sql
SELECT DISTINCT ON (location) location, time, report FROM 
weather_reports ORDER BY location, time DESC;
```
retrieves the most recent weather report for each location. But if we had not used `ORDER BY` to force descending order of time values for each location, we would have gotten a report from an unpredictable time for each location.

The `DISTINCT ON` expression(s) must match the left-most `ORDER BY` expression(s). The `ORDER BY` clause will normally contain additional expression(s) that determine the desired precedence of rows within each `DISTINCT ON` group.

When the database processes queries that contain the `DISTINCT` clause, the queries are transformed into `GROUP BY` queries. In many cases, the transformation provides significant performance gains. However, when the number of distinct values is close to the total number of rows, the transformation might result in the generation of a multi-level grouping plan. In this case, there is an expected performance degradation because of the overhead introduced by the lower aggregation level.

### LIMIT clause
The `LIMIT` clause consists of two independent subclauses:
```sql
LIMIT {count | ALL}
OFFSET start
```
where `count` specifies the maximum number of rows to return, while `start` specifies the number of rows to skip before starting to return rows. When both are specified, `start` rows are skipped before starting to count the `count` rows to be returned.

When using `LIMIT`, it is a good idea to use an `ORDER BY` clause that constrains the result rows into a unique order. Otherwise you will get an unpredictable subset of the query's rows — you may be asking for the tenth through twentieth rows, but tenth through twentieth in what ordering? You don't know what ordering unless you specify `ORDER BY`.

The query optimizer takes `LIMIT` into account when generating a query plan, so you are very likely to get different plans (yielding different row orders) depending on what you use for `LIMIT` and `OFFSET`. Thus, using different `LIMIT/OFFSET` values to select different subsets of a query result will give inconsistent results unless you enforce a predictable result ordering with `ORDER BY`. This is not a defect; it is an inherent consequence of the fact that SQL does not promise to deliver the results of a query in any particular order unless `ORDER BY` is used to constrain the order.

### FOR UPDATE/FOR SHARE clause
The `FOR UPDATE` clause has this form:
```sql
FOR UPDATE [OF table_name [, ...]] [NOWAIT]
```
The closely related `FOR SHARE` clause has this form:
```sql
FOR SHARE [OF table_name [, ...]] [NOWAIT]
```

`FOR UPDATE` causes the tables accessed by the `SELECT` statement to be locked as though for update. This prevents the table from being modified or deleted by other transactions until the current transaction ends. That is, other transactions that attempt `UPDATE`, `DELETE`, or `SELECT FOR UPDATE` of this table will be blocked until the current transaction ends. Also, if an `UPDATE`, `DELETE`, or `SELECT FOR UPDATE` from another transaction has already locked a selected table, `SELECT FOR UPDATE` will wait for the other transaction to complete, and will then lock and return the updated table.

To prevent the operation from waiting for other transactions to commit, use the `NOWAIT` option. With `NOWAIT`, the statement reports an error, rather than waiting, if a selected row cannot be locked immediately.

Note that `NOWAIT` applies only to the row-level lock — the required `ROW SHARE` table-level lock is still taken in the ordinary way. You can use `LOCK` with the `NOWAIT` option first, if you need to acquire the table-level lock without waiting (see **LOCK**).

`FOR SHARE` behaves similarly, except that it acquires a shared rather than exclusive lock on the table. A shared lock blocks other transactions from performing `UPDATE`, `DELETE`, or `SELECT FOR UPDATE` on the table, but it does not prevent them from performing `SELECT FOR SHARE`.

If specific tables are named in `FOR UPDATE` or `FOR SHARE`, then only those tables are locked; any other tables used in the `SELECT` are simply read as usual. A `FOR UPDATE` or `FOR SHARE` clause without a table list affects all tables used in the command. If `FOR UPDATE` or `FOR SHARE` is applied to a view or subquery, it affects all tables used in the view or subquery.

`FOR UPDATE` or `FOR SHARE` do not apply to a `with_query` referenced by the primary query. If you want row locking to occur within a `with_query`, specify `FOR UPDATE` or `FOR SHARE` within the `with_query`.

Multiple `FOR UPDATE` and `FOR SHARE` clauses can be written if it is necessary to specify different locking behavior for different tables. If the same table is mentioned (or implicitly affected) by both `FOR UPDATE` and `FOR SHARE` clauses, then it is processed as `FOR UPDATE`. Similarly, a table is processed as `NOWAIT` if that is specified in any of the clauses affecting it.

## Examples
To join the table `films` with the table `distributors`:
```sql
SELECT f.title, f.did, d.name, f.date_prod, f.kind FROM 
distributors d, films f WHERE f.did = d.did
```
To sum the column `length` of all films and group the results by `kind`:
```sql
SELECT kind, sum(length) AS total FROM films GROUP BY kind;
```
To sum the column `length` of all films, group the results by `kind`, and show those group totals that are less than 5 hours:
```sql
SELECT kind, sum(length) AS total FROM films GROUP BY kind 
HAVING sum(length) < interval '5 hours';
```
To calculate the subtotals and grand totals of all sales for films by `kind` and `distributor`:
```sql
SELECT kind, distributor, sum(prc*qty) FROM sales
GROUP BY ROLLUP(kind, distributor)
ORDER BY 1,2,3;
```
To calculate the rankings of film distributors based on total sales:
```sql
SELECT distributor, sum(prc*qty), 
       rank() OVER (ORDER BY sum(prc*qty) DESC) 
FROM sale
GROUP BY distributor ORDER BY 2 DESC;
```
The following two examples are identical ways of sorting the individual results according to the contents of the second column (name):
```sql
SELECT * FROM distributors ORDER BY name;
SELECT * FROM distributors ORDER BY 2;
```
The next example shows how to obtain the union of the tables `distributors` and `actors`, restricting the results to those that begin with the letter W in each table. Only distinct rows are wanted, so the keyword `ALL` is omitted.
```sql
SELECT distributors.name FROM distributors WHERE 
distributors.name LIKE 'W%' UNION SELECT actors.name FROM 
actors WHERE actors.name LIKE 'W%';
```
This example shows how to use a function in the `FROM` clause, both with and without a column definition list:
```sql
CREATE FUNCTION distributors(int) RETURNS SETOF distributors 
AS $$ SELECT * FROM distributors WHERE did = $1; $$ LANGUAGE 
SQL;
SELECT * FROM distributors(111);
 
CREATE FUNCTION distributors_2(int) RETURNS SETOF record AS 
$$ SELECT * FROM distributors WHERE did = $1; $$ LANGUAGE 
SQL;
SELECT * FROM distributors_2(111) AS (dist_id int, dist_name 
text);
```
This example shows how to use a simple `WITH` clause:
```sql
WITH test AS (
  SELECT random() as x FROM generate_series(1, 3)
  )
SELECT * FROM test
UNION ALL
SELECT * FROM test; 
```
This example uses the `WITH` clause to display per-product sales totals in only the top sales regions.
```sql
WITH regional_sales AS 
    SELECT region, SUM(amount) AS total_sales
    FROM orders
    GROUP BY region
  ), top_regions AS (
    SELECT region
    FROM regional_sales
    WHERE total_sales > (SELECT SUM(total_sales) FROM
       regional_sales)
  )
SELECT region, product, SUM(quantity) AS product_units,
   SUM(amount) AS product_sales
FROM orders
WHERE region IN (SELECT region FROM top_regions) 
GROUP BY region, product;
```
The example could have been written without the `WITH` clause but would have required two levels of nested sub-`SELECT` statements.

## Compatibility
The `SELECT` statement is compatible with the SQL standard, but there are some extensions and some missing features.

**Omitted `FROM` clauses**
The database allows one to omit the `FROM` clause. It has a straightforward use to compute the results of simple expressions. For example:
```sql
SELECT 2+2;
```
Some other SQL databases cannot do this except by introducing a dummy one-row table from which to do the `SELECT`.

Note that if a `FROM` clause is not specified, the query cannot reference any database tables. For compatibility with applications that rely on this behavior the `add_missing_from` configuration variable can be enabled.

**`AS` Keyword**
In the SQL standard, the optional keyword `AS` is just noise and can be omitted without affecting the meaning. The database parser requires this keyword when renaming output columns because the type extensibility features lead to parsing ambiguities without it. The optional keyword `AS` can be omitted before an output column name whenever the new column name is a valid column name (that is, not the same as any reserved keyword). 

PostgreSQL is slightly more restrictive: `AS` is required if the new column name matches any keyword at all, reserved or not. Recommended practice is to use `AS` or double-quote output column names, to prevent any possible conflict against future keyword additions. `AS` is optional in `FROM` items, however.

**Namespace Available to `GROUP BY` and `ORDER BY`**
In the SQL-92 standard, an `ORDER BY` clause may only use result column names or numbers, while a `GROUP BY` clause may only use expressions based on input column names. The database extends each of these clauses to allow the other choice as well (but it uses the standard's interpretation if there is ambiguity). The database also allows both clauses to specify arbitrary expressions. Note that names appearing in an expression are always taken as input column names, not as result column names.

SQL:1999 and later use a slightly different definition which is not entirely upward compatible with SQL-92. In most cases, however, the database interprets an `ORDER BY` or `GROUP BY` expression the same way SQL:1999 does.

**Nonstandard Clauses**
The clauses `DISTINCT ON`, `LIMIT`, and `OFFSET` are not defined in the SQL standard.

**Limited Use of `STABLE` and `VOLATILE` Functions**
To prevent data from becoming out-of-sync across the segments in the database, any function classified as `STABLE` or `VOLATILE` cannot be executed at the segment database level if it contains SQL or modifies the database in any way.

## See Also
EXPLAIN
