This document describes the supported statement scenarios and restricted scenarios of the parallel query.

[](id:JRYJCJ1)
## Supported statement scenarios
TencentDB for MySQL has implemented the parallel query feature for SQL statements with the following characteristics, with more to come.
- Single-table scan: Full-table scan, index scan, index range scan, and index REF query in ascending or descending order are supported.
- Multi-table join: The nested-loop join (NLJ) algorithm as well as semi join, anti join, and outer join are supported.
- Subquery: Parallel query is supported for derived tables.
- Data type: Different data types can be queried, such as integer, string, floating point, time, and overflow (with a runtime size limit).
- There are no restrictions on common operators and functions.
- COUNT, SUM, AVG, MIN, and MAX aggregate functions are supported.
- UNION and UNION ALL queries are supported.
- Traditional (default), JSON, and tree EXPLAIN formats are supported.

## Restricted scenarios
The parallel query feature of TencentDB for MySQL is not supported in the following scenarios.

<table>
<thead><tr><th>Restriction</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td rowspan="6">Statement compatibility restriction</td>
<td>Parallel query is not supported for non-query statements, including `INSERT ... SELECT` and `REPLACE ... SELECT`.</td></tr>
<tr><td>Parallel query is not supported for statements in a stored program.</td></tr>
<tr><td>Parallel query is not supported for prepared statements.</td></tr>
<tr><td>Parallel query is not supported for statements in serial isolation-level transactions.</td></tr>
<tr><td>Parallel query is not supported for locking reads, such as `SELECT FOR UPDATE` and `SELECT ... FOR SHARE`.</td></tr>
<tr><td>Parallel query is not supported for CTEs.</td></tr>
<tr>
<td rowspan="5">Table/Index compatibility restriction</td>
<td>Parallel query is not supported for system, temp, and non-InnoDB tables.</td></tr>
<tr><td>Parallel query is not supported for space index.</td></tr>
<tr><td>Parallel query is not supported for full-text index.</td></tr>
<tr><td>Parallel query is not supported for partitioned tables.</td></tr>
<tr><td>Parallel query is not supported for tables in `index_merge` scan mode.</td></tr>
<tr>
<td rowspan="13">Expression/Field compatibility restriction</td>
<td>Parallel query is not supported for tables containing generated columns or BLOB, TEXT, JSON, BIT, and GEOMETRY fields.</td></tr>
<tr><td>Parallel query is not supported for aggregate functions of the BIT_AND, BIT_OR, or BIT_XOR type.</td></tr>
<tr><td>Parallel query is not supported for DISTINCT aggregations, such as SUM(DISTINCT) and COUNT(DISTINCT).</td></tr>
<tr><td>Parallel query is not supported for GIS functions such as SP_WITHIN_FUNC and ST_DISTANCE.</td></tr>
<tr><td>Parallel query is not supported for custom functions.</td></tr>
<tr><td>Parallel query is not supported for JSON functions such as JSON_LENGTH, JSON_TYPE, and JSON_ARRAYAGG.</td></tr>
<tr><td>Parallel query is not supported for XML functions such as XML_STR.</td></tr>
<tr><td>Parallel query is not supported for user-lock functions such as IS_FREE_LOCK, IS_USED_LOCK, RELEASE_LOCK, RELEASE_ALL_LOCKS, and GET_LOCK.</td></tr>
<tr><td>Parallel query is not supported for SLEEP, RANDOM, GROUP_CONCAT, SET_USER_VAR, and WEIGHT_STRING functions.</td></tr>
<tr><td>Parallel query is not supported for certain statistical functions such as STD, STDDEV, STDDEV_POP, VARIANCE, VAR_POP, and VAR_SAMP.</td></tr>
<tr><td>Parallel query is not supported for subqueries.</td></tr>
<tr><td>Parallel query is not supported for window functions.</td></tr>
<tr><td>Parallel query is not supported for ROLLUP.</td></tr>
</tbody></table>	

Besides the above examples in [Supported statement scenarios](#JRYJCJ1), you can also check the parallel query execution plan and thread working status to see whether a statement can be queried parallelly. For more information, see [Viewing Parallel Query](https://www.tencentcloud.com/document/product/236/53411).

