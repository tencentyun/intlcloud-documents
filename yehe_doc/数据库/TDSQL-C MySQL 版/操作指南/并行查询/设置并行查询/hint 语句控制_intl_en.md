TDSQL-C for MySQL allows you to enable or disable the parallel query feature by adjusting parameters. Specifically, you can enable or disable the feature for all SQL statements, set execution conditions, or specify the execution mode of a specific SQL statement through the HINT statement in the console.
>? The HINT statement can specify whether to execute a SQL statement and apply session parameters to the statement. In addition, it also supports querying the specified parallel table.
>

## HINT statement usage

| Feature | Command Line | Description |
|---------|---------|---------|
| Enable parallel query | `SELECT /*+PARALLEL(x)*/ ... FROM ...;` | `x` indicates the parallelism for the SQL statement, which should be greater than `0`. |
| Disable parallel query | `SELECT /*+PARALLEL(x)*/ ... FROM ...;` | If `x` is set to `0`, it indicates to disable parallel query. |
| Specify the parallel table | You can specify the table to be included in or excluded from the parallel query execution plan in either of the following ways: <li>Specify the table to be included in the plan through `PARALLEL`. <br>`SELECT /*+PARALLEL(t)*/ ... FROM ...;`<li>Specify the table to be excluded from the plan through `NO_PARALLEL`. <br>`SELECT /*+NO_PARALLEL(t)*/ ... FROM ...;` | `t` is the table name. |
| Specify both the parallel table and parallelism | `SELECT /*+PARALLEL(t x)*/ * ... FROM ...;` | `x` indicates the parallelism for the SQL statement, which should be greater than `0`. `t` is the table name. |
| Set the session parameter through the HINT statement, which takes effect only for the specified SQL statement | `SELECT /*+SET_VAR(var=n)*/ * ... FROM ...;` | `var` is the parallel query parameter in the `session` scope. |

## HINT statement use cases
**Use case 1:**
`select /*+PARALLEL()*/ * FROM t1,t2;`
Set the parallelism to the value of `txsql_parallel_degree` (default) for the parallel query. If a statement does not meet the parallel query execution condition, serial query will be used.

**Use case 2:**
`select /*+PARALLEL(4)*/ * FROM t1,t2;`
Set the parallelism of the statement to `4` regardless of the default value, i.e., `txsql_parallel_degree = 4`. If the statement does not meet the parallel query execution condition, serial query will be used.

**Use case 3:**
`select /*+PARALLEL(t1)*/ * FROM t1,t2;`
Include the `t1` table in the parallel query and use the default parallelism. If `t1` is smaller than the value of `txsql_parallel_table_record_threshold`, serial query will be used.

**Use case 4:**
`select /*+PARALLEL(t1 8)*/ * FROM t1,t2;`
Include the `t1` table in the parallel query and set the parallelism to `8`. If `t1` is smaller than the value of `txsql_parallel_table_record_threshold`, serial query will be used.

**Use case 5:**
`select /*+NO_PARALLEL(t1)*/ * FROM t1,t2;`
Exclude the `t1` table from the parallel query. If `t1` is greater than the value of `txsql_parallel_table_record_threshold`, serial query will be used.

**Use case 6:**
`select /*+SET_VAR(txsql_parallel_degree=8)*/ * FROM t1,t2;`
Set the parallelism of the statement to `8` regardless of the default value, i.e., `txsql_parallel_degree = 8`.

**Use case 7:**
`select /*+SET_VAR(txsql_parallel_cost_threshold=1000)*/ * FROM t1,t2`
Set `txsql_parallel_cost_threshold=1000` for the statement. If its execution penalty is greater than `1000`, parallel query can be used.

**Use case 8:**
`select /*+SET_VAR(txsql_optimizer_context_max_mem_size=500000)*/ * FROM t1,t2`
Set `txsql_optimizer_context_max_mem_size=500000` for a statement, which means to adjust the maximum memory size it can apply for in the parallel query plan environment to `500000`.

## References
- [Enabling/Disabling Parallel Query](https://www.tencentcloud.com/document/product/1098/51769)
- [Viewing Parallel Query](https://www.tencentcloud.com/document/product/1098/51764)
- [Parallel Query Metrics](https://www.tencentcloud.com/document/product/1098/51763)
