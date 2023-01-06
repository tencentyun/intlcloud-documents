TDSQL-C for MySQL allows you to view the parallel query execution plan and threads in the plan, so that you can clearly know how parallel query takes effect in a database and quickly troubleshoot issues.
This document describes two common methods for viewing parallel queries.

## Option 1: Using the EXPLAIN statement
**Sample SQL statement:**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
This sample is a simplified version of TPC-H Q1, a typical report operation.

**EXPLAIN statement:**
```
EXPLAIN  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**Query result:**
```
MySQL [tpch100g]> explain SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '1998-09-02' GROUP BY l_returnflag, l_linestatus ORDER BY l_returnflag, l_linestatus;
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
| id | select_type | table       | partitions | type | possible_keys | key  | key_len | ref  | rows      | filtered | Extra                                                     |
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
|  1 | SIMPLE      | lineitem    | NULL       | ALL  | i_l_shipdate  | NULL | NULL    | NULL | 593184480 |    50.00 | Parallel scan (4 workers); Using where; Using temporary   |
|  1 | SIMPLE      | <sender1>   | NULL       | ALL  | NULL          | NULL | NULL    | NULL |         0 |     0.00 | Send to (<receiver1>)                                     |
|  1 | SIMPLE      | <receiver1> | NULL       | ALL  | NULL          | NULL | NULL    | NULL |         0 |     0.00 | Receive from (<sender1>); Using temporary; Using filesort |
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
3 rows in set, 1 warning (0.00 sec)
```
**EXPLAIN format=tree:**
```
EXPLAIN format=tree query  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**Query result:**
```
MySQL [tpch100g]> explain format=tree SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '1998-09-02' GROUP BY l_returnflag, l_linestatus ORDER BY l_returnflag, l_linestatus\G
*************************** 1. row ***************************
EXPLAIN: -> Sort: lineitem.L_RETURNFLAG, lineitem.L_LINESTATUS
    -> Table scan on <temporary>
        -> Final Aggregate using temporary table
            -> PX Receiver (slice: 0; workers: 1)
                -> PX Sender (slice: 1; workers: 4)
                    -> Table scan on <temporary>
                        -> Aggregate using temporary table
                            -> Filter: (lineitem.L_SHIPDATE <= DATE'1998-09-02')  (cost=65449341.10 rows=296592240)
                                -> Parallel table scan on lineitem  (cost=65449341.10 rows=593184480)

1 row in set (0.00 sec)
```
As can be seen from the above result:
- The parallel query plan assigns the statement to four worker threads for computing.
- Aggregate operations are split into two segments that are executed by the user and parallel threads respectively.
- The parallel scan operator is used for the `lineitem` table.
- EXPLAIN format=tree query works better than the traditional EXPLAIN.

## Option 2: Viewing in the thread list
The result of the `show processlist` command displays which threads are running. You can view not only the total number of current connections but also the connection status to identify abnormal query statements.
Based on the `show processlist` command, TDSQL-C for MySQL offers the proprietary `show parallel processlist` statement, which displays only the threads related to parallel query and filters out irrelevant threads.
**Sample SQL statement:**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
This sample is a simplified version of TPC-H Q1, a typical report operation.
**`show processlist` query result:**
```
mysql> show processlist;
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
| Id     | User        | Host            | db        | Command | Time  | State      | Info                                                                                                 |
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
|      7 | tencentroot | 127.0.0.1:49238 | NULL      | Sleep   |     0 |            | NULL                                                                                                 |
|     11 | tencentroot | 127.0.0.1:49262 | NULL      | Sleep   |     0 |            | NULL                                                                                                 |
|     13 | tencentroot | 127.0.0.1:49288 | NULL      | Sleep   |     1 |            | NULL                                                                                                 |
| 237062 | tencentroot | localhost       | tpch100g  | Query   |    24 | Scheduling | SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '199 |
| 237107 | tencentroot | localhost       | NULL      | Query   |     0 | init       | show processlist                                                                                     |
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
6 rows in set (0.00 sec)
```
**`show parallel processlist` query result:**
```
mysql> show parallel processlist;
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
| Id     | User        | Host      | db       | Command | Time | State       | Info                                                                                                 |
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
| 237062 | tencentroot | localhost | tpch100g | Query   |   18 | Scheduling  | SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '199 |
| 237110 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 0, task 1                                                                  |
| 237111 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 1, task 1                                                                  |
| 237112 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 2, task 1                                                                  |
| 237113 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 3, task 1                                                                  |
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
5 rows in set (0.00 sec)
```

As can be seen from the above result:
- The parallel query plan assigns queries to four worker threads. There is only one data item in the user thread (ID: 237062). The SQL statement is pushed down to four worker threads. As indicated in `info`, all these four threads are executing `task 1`.
- Each thread can be identified and located precisely.
- Compared to `show processlist`, `show parallel processlist` can precisely find all running threads of parallel query and will not be affected by other threads.

## References
- [Enabling/Disabling Parallel Query](https://www.tencentcloud.com/document/product/1098/51769)
- [HINT Statement Control](https://www.tencentcloud.com/document/product/1098/51765)
- [Parallel Query Metrics](https://www.tencentcloud.com/document/product/1098/51763)

