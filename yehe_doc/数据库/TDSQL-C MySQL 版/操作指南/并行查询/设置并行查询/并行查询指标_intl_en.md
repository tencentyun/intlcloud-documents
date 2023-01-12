This document describes the monitoring metrics offered by TDSQL-C for MySQL to help you monitor the operations related to parallel database query in real time.

## Prerequisites
Database version: TDSQL-C for MySQL 8.0 on kernel version 3.1.8 or later.

## Parallel query monitoring metrics

| Metric | Parameter | Unit | Description | Data Aggregation Method |
|---------|---------|---------|---------|---------|
| Parallelly Queried Threads | txsql_parallel_threads_currently_used | - | The number of threads currently used for parallel queries. | MAX |
| Failed Parallel Queries | txsql_parallel_stmt_error | - | The number of parallel query statements that report errors. | SUM |
| Executed Parallel Queries | txsql_parallel_stmt_executed | - | The number of executed parallel query statements. | SUM |
| Parallel-to-Serial Queries | txsql_parallel_stmt_fallback | - | The number of parallel-to-serial query statements. | SUM |

## Best practices for monitoring
The following lists some special issues for which you should check the metrics and their solutions.
**Example 1:**
The value of **Parallelly Queried Threads** is always equal to the value set by `txsql_max_parallel_worker_threads`.
**Solution:**
This example indicates that the threads are always fully loaded. We recommend you increase the value of the `txsql_max_parallel_worker_threads` parameter when the CPU utilization is low.

**Example 2:**
The value of **Failed Parallel Queries** increases.
**Solution:**
Check the CPU utilization and memory utilization. If the load becomes significantly higher, we recommend you reduce the value of `txsql_parallel_degree` to 1/4 of the number of CPU cores.

**Example 3:**
The value of **Parallel-to-Serial Queries** increases.
**Solution:**
This example indicates that the currently executed SQL statement does not meet the conditions for parallel query. We recommend you increase the total number of threads (`txsql_max_parallel_worker_threads`) or the maximum memory (`txsql_optimizer_context_max_mem_size`) of the parallel query plan environment that a single statement can apply for, so as to ensure that parallel query can be used for SQL statements.
