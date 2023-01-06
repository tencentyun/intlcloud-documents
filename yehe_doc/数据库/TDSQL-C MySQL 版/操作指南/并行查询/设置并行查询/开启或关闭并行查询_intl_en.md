This document describes how to enable or disable the parallel query feature of TDSQL-C for MySQL via the console or command line.

## Prerequisites
Database version: TDSQL-C for MySQL 8.0 on kernel version 3.1.8 or later.

## Parameters
>? The parallel query feature can be enabled for both read-write and read-only instances, as long as their number of CPU cores is greater than or equal to 4.

You can enable the parallel query feature for the current instance by setting the `txsql_max_parallel_worker_threads` and `txsql_parallel_degree` parameters to a value other than `0` via the console or command line. Parameters and suggested settings are as follows:
**Parameter information**

| Parameter | Variable Type | Scope | Default Value | Value Range | Description |
|---------|---------|---------|---------|---------|---------|
| txsql_max_parallel_worker_threads | Integer | Global | 0 | 0–1024 | The total number of threads of the instance node that can be used for parallel query. If it is set to `0`, no parallel thread is available, indicating to disable the parallel query feature. |
| txsql_parallel_degree | Integer | Global/session | 0 | 0–1024 | The maximum number of threads (default parallelism) that can be used during the parallel query of a single statement. `0` indicates to disable the parallel query feature. |

**Suggested settings**
- Parallelism limit: `txsql_parallel_degree` indicates the maximum number of threads for the parallel query of a single statement, i.e., the default parallelism. We recommend you limit this value to half of the CPU core quantity of the instance. To ensure the stability, the parallel query feature is disabled for small clusters with fewer than four CPU cores, and you cannot adjust parallel query parameters via the console or command line.
- During the parallel query of a SQL statement, the parallelism set by `txsql_parallel_degree` will be used by default, which can be adjusted through the HINT statement. For more information, see [HINT Statement Control](https://www.tencentcloud.com/document/product/1098/51765).
- `txsql_max_parallel_worker_threads` indicates the number of threads of the instance that can be used for parallel query, and `txsql_max_parallel_worker_threads / txsql_parallel_degree` indicates the maximum number of SQL statements allowed in a parallel query.
- `txsql_max_parallel_worker_threads` and `txsql_parallel_degree` control the status of the parallel query feature. When either of them is `0`, the feature is disabled.

TDSQL-C for MySQL offers various parameters for you to set the execution conditions of parallel query for business adaptation and stability. After conditions are set, TDSQL-C for MySQL will check whether each SQL statement can be executed against such conditions like execution cost, number of table rows, and memory usage for the parallel statement execution. Parameters are described as follows:

| Parameter | Variable Type | Scope | Default Value | Value Range | Description |
|---------|---------|---------|---------|---------|---------|
| txsql_parallel_cost_threshold | Numeric | Global/Session | 50000 | 0–9223372036854775807 | The threshold of parallel execution cost. Only statements with an execution cost higher than this threshold will be executed parallelly. |
| txsql_parallel_table_record_threshold | Integer | Global/Session | 5000 |0–9223372036854775807 | The threshold of parallel table row quantity. Only tables with a row quantity higher than this threshold will be selected as parallel tables. |
| txsql_optimizer_context_max_mem_size | Integer | Global | 8388608 | 0–9223372036854775807 | The maximum memory size that a single statement can apply for in the parallel query plan environment. |
| txsql_parallel_execution_max_lob_size | Integer | Global/Session | 65536 | 128–9223372036854775807 | The memory limit of a single overflow field. |

>!
>- Parallel query parameters take effect immediately after being set, with no instance restart required.
>- If the scope of a parameter is session, it takes effect only for the statement.

### Enabling or disabling parallel query in the console
You can enable or disable the feature by setting parameters on the **Parameter Settings** page in the TDSQL-C for MySQL console.
- Set `txsql_max_parallel_worker_threads` and `txsql_parallel_degree` to a value other than `0` to enable parallel query.
- Set `txsql_max_parallel_worker_threads` or `txsql_parallel_degree` to `0` to disable parallel query.

You can also set execution conditions on the **Parameter Settings** page. For detailed directions, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/1098/44602).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/T9dd323_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16729160029226.png)

### Specifying the parallel execution mode of a SQL statement through the HINT statement
TDSQL-C for MySQL allows you to specify the parallel execution mode of a SQL statement through the HINT statement. For detailed directions, see [HINT Statement Control](https://www.tencentcloud.com/document/product/1098/51765).

## References
- [Viewing Parallel Query](https://www.tencentcloud.com/document/product/1098/51764)
- [Parallel Query Metrics](https://www.tencentcloud.com/document/product/1098/51763)
