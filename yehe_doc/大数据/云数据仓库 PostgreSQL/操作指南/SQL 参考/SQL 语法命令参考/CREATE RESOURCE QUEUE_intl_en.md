It defines a new resource queue.

## Synopsis
```sql
CREATE RESOURCE QUEUE name WITH (queue_attribute=value [, ... ])
```

where `queue_attribute` is:

```sql
    ACTIVE_STATEMENTS=integer
        [ MAX_COST=float [COST_OVERCOMMIT={TRUE|FALSE}] ]
        [ MIN_COST=float ]
        [ PRIORITY={MIN|LOW|MEDIUM|HIGH|MAX} ]
        [ MEMORY_LIMIT='memory_units' ]
 
 | MAX_COST=float [ COST_OVERCOMMIT={TRUE|FALSE} ]
        [ ACTIVE_STATEMENTS=integer ]
        [ MIN_COST=float ]
        [ PRIORITY={MIN|LOW|MEDIUM|HIGH|MAX} ]
        [ MEMORY_LIMIT='memory_units' ]
```

## Description
It creates a new resource queue for database resource management. A resource queue must have either an `ACTIVE_STATEMENTS` or a `MAX_COST` value (or it can have both). Only a superuser can create a resource queue.

Resource queues with an `ACTIVE_STATEMENTS` threshold set a maximum limit on the number of queries that can be executed by roles assigned to that queue. It controls the number of active queries that are allowed to run at the same time. The value for `ACTIVE_STATEMENTS` should be an integer greater than 0.

Resource queues with a `MAX_COST` threshold set a maximum limit on the total cost of queries that can be executed by roles assigned to that queue. Cost is measured in the **estimated total cost** for the query as determined by the database query planner (as shown in the `EXPLAIN` output for a query).

Therefore, an administrator must be familiar with the queries typically executed on the system in order to set an appropriate cost threshold for a queue. Cost is measured in units of disk page fetches; 1.0 equals one sequential disk page read. The value for `MAX_COST` is specified as a floating point number (for example 100.0) or can also be specified as an exponent (for example 1e+2).

If a resource queue is limited based on a cost threshold, then the administrator can allow `COST_OVERCOMMIT = TRUE` (the default). This means that a query that exceeds the allowed cost threshold will be allowed to run but only when the system is idle. If `COST_OVERCOMMIT = FALSE` is specified, queries that exceed the cost limit will always be rejected and never allowed to run. Specifying a value for `MIN_COST` allows the administrator to define a cost for small queries that will be exempt from resource queuing.

If a value is not defined for `ACTIVE_STATEMENTS` or `MAX_COST`, it is set to -1 by default (meaning no limit). After defining a resource queue, you must assign roles to the queue using the [`ALTER ROLE`](https://gp-docs-cn.github.io/docs/ref_guide/sql_commands/ALTER_ROLE.html#topic1) or [`CREATE ROLE`](https://gp-docs-cn.github.io/docs/ref_guide/sql_commands/CREATE_ROLE.html#topic1) command.

You can optionally assign a `PRIORITY` to a resource queue to control the relative share of available CPU resources used by queries associated with the queue in relation to other resource queues. If a value is not defined for `PRIORITY`, queries associated with the queue have a default priority of `MEDIUM`.

Resource queues with an optional `MEMORY_LIMIT` threshold set a maximum limit on the amount of memory that all queries submitted through a resource queue can consume on a segment host. This determines the total amount of memory that all worker processes of a query can consume on a segment host during query execution. The database recommends that `MEMORY_LIMIT` be used in conjunction with `ACTIVE_STATEMENTS` rather than with `MAX_COST`.
- The default amount of memory allotted per query on statement-based queues is: MEMORY_LIMIT / ACTIVE_STATEMENTS.
- The default amount of memory allotted per query on cost-based queues is: MEMORY_LIMIT * (query_cost / MAX_COST).

The default memory allotment can be overridden on a per-query basis using the `statement_mem` server configuration parameter, provided that `MEMORY_LIMIT` or `max_statement_mem` is not exceeded. For example, to allocate more memory to a particular query:
```sql
=> SET statement_mem='2GB';
=> SELECT * FROM my_big_table WHERE column='value' ORDER BY id;
=> RESET statement_mem;
```

The `MEMORY_LIMIT` value for all of your resource queues should not exceed the amount of physical memory of a segment host. If workloads are staggered over multiple queues, memory allocations can be oversubscribed. However, queries can be canceled during execution if the segment host memory limit specified in `gp_vmem_protect_limit` is exceeded.

## Parameters
name
The name of the resource queue.

ACTIVE_STATEMENTS integer
Resource queues with an `ACTIVE_STATEMENTS` threshold limit the number of queries that can be executed by roles assigned to that queue. It controls the number of active queries that are allowed to run at the same time. The value for `ACTIVE_STATEMENTS` should be an integer greater than 0.

MEMORY_LIMIT 'memory_units'
Sets the total memory quota for all statements submitted from users in this resource queue. Memory units can be specified in KB, MB or GB. The minimum memory quota for a resource queue is 10 MB. There is no maximum, however the upper boundary at query execution time is limited by the physical memory of a segment host. The default is no limit (-1).

MAX_COST float
Resource queues with a `MAX_COST` threshold set a maximum limit on the total cost of queries that can be executed by roles assigned to that queue. Cost is measured in the \*estimated total cost\* for the query as determined by the database query optimizer (as shown in the `EXPLAIN` output for a query). Therefore, an administrator must be familiar with the queries typically executed on the system in order to set an appropriate cost threshold for a queue. Cost is measured in units of disk page fetches; 1.0 equals one sequential disk page read. The value for `MAX_COST` is specified as a floating point number (for example 100.0) or can also be specified as an exponent (for example 1e+2).

COST_OVERCOMMIT boolean
If a resource queue is limited based on `MAX_COST`, then the administrator can allow `COST_OVERCOMMIT` (the default). This means that a query that exceeds the allowed cost threshold will be allowed to run but only when the system is idle. If `COST_OVERCOMMIT = FALSE` is specified, queries that exceed the cost limit will always be rejected and never allowed to run.

MIN_COST float
The minimum query cost limit of what is considered a small query. Queries with a cost under this limit will not be queued and run immediately. Cost is measured in the \*estimated total cost\* for the query as determined by the database query planner (as shown in the `EXPLAIN` output for a query). Therefore, an administrator must be familiar with the queries typically executed on the system in order to set an appropriate cost for what is considered a small query. Cost is measured in units of disk page fetches; 1.0 equals one sequential disk page read. The value for `MIN_COST` is specified as a floating point number (for example 100.0) or can also be specified as an exponent (for example 1e+2).

PRIORITY={MIN|LOW|MEDIUM|HIGH|MAX}
Sets the priority of queries associated with a resource queue. Queries or statements in queues with higher priority levels will receive a larger share of available CPU resources in case of contention. Queries in low-priority queues may be delayed while higher priority queries are executed. If no priority is specified, queries associated with the queue have a priority of `MEDIUM`.

## Notes
Use the `gp_toolkit.gp_resqueue_status` system view to see the limit settings and current status of a resource queue:
```sql
SELECT * from gp_toolkit.gp_resqueue_status WHERE 
  rsqname='queue_name';
```
There is also another system view named `pg_stat_resqueues` which shows statistical metrics for a resource queue over time. To use this view, however, you must enable the `stats_queue_level` server configuration parameter. See "Managing Workload and Resources" in the Database Administrator Guide for more information about using resource queues.

`CREATE RESOURCE QUEUE` cannot be run within a transaction.

Also, an SQL statement that is run during the execution of an `EXPLAIN ANALYZE` command is excluded from resource queues.

## Examples
Create a resource queue with an active query limit of 20:
```sql
CREATE RESOURCE QUEUE myqueue WITH (ACTIVE_STATEMENTS=20);
```
Create a resource queue with an active query limit of 20 and a total memory limit of 2000 MB (each query will be allocated 100 MB of segment host memory at execution time):
```sql
CREATE RESOURCE QUEUE myqueue WITH (ACTIVE_STATEMENTS=20, 
  MEMORY_LIMIT='2000MB');
```
Create a resource queue with a query cost limit of 3000.0:
```sql
CREATE RESOURCE QUEUE myqueue WITH (MAX_COST=3000.0);
```
Create a resource queue with a query cost limit of 3^10 (or 30000000000.0) and do not allow overcommit. Allow small queries with a cost under 500 to run immediately:
```sql
CREATE RESOURCE QUEUE myqueue WITH (MAX_COST=3e+10, 
  COST_OVERCOMMIT=FALSE, MIN_COST=500.0);
```
Create a resource queue with both an active query limit and a query cost limit:
```sql
CREATE RESOURCE QUEUE myqueue WITH (ACTIVE_STATEMENTS=30, 
  MAX_COST=5000.00);
```
Create a resource queue with an active query limit of 5 and a maximum priority setting:
```sql
CREATE RESOURCE QUEUE myqueue WITH (ACTIVE_STATEMENTS=5, 
  PRIORITY=MAX);
```

## Compatibility
`CREATE RESOURCE QUEUE` is a database extension. There is no provision for resource queues or resource management in the SQL standard.

## See Also
ALTER ROLE, CREATE ROLE, ALTER RESOURCE QUEUE, DROP RESOURCE QUEUE
