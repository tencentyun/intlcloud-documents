
## Overview
Performance test is a comprehensive analysis service for database instance performance and health. It can analyze SQL statement performance, CPU utilization, IOPS utilization, memory utilization, disk utilization, connections, locks, hotspot tables, and transactions, helping you identify and address existing and potential health issues in your database through smart diagnosis and optimization.

>?For certain test items, the performance test report provides a series of optimization suggestions. Please carefully test the suggested measures before applying them so as to prevent the instance performance problems from getting worse.

## Features
**Health rating:** you can view the current database performance score out of 100 points. If your database scores below 60 for a long time, please optimize your business or database configuration.
**Report generation, viewing, and saving:** you can create a report or view the last report as desired. The report can be saved as a webpage for download.

Performance test mainly includes the following features:
#### Resource analysis
Analyzes the usage of database instance resources (CPU, disk, and connections) in a certain period of time and displays an overall score.
>?As most instances have an "overuse when idle" policy enabled by default, you may observe that the maximum CPU utilization exceeds 100%. If this is persistent and the average is higher than the recommended value, you are recommended to scale your instance up.

#### System status
Sorts out key instance metrics, lists their status and time of occurrence, and suggests corresponding modifications.

#### Tablespace distribution
Lists the current top 10 tables in reverse order in terms of data space to help you identify oversized tables.

#### Redundant index detection
Lists the current possible redundant indexes (whose selectivity is below 1%) and suggests optimizations.

>?Because a query statement must first query the indices before querying tables through indices, if there are too many identical data entries in the index column, the performance to reduce the amount of data to be filtered may be compromised and is not as fast as full table scan.

#### Deadlock diagnosis
The deadlock diagnosis gets the information of the last deadlock in the database through `show engine innodb status` and displays it if the deadlock occurs within the selected diagnostic time period.

>?If deadlock occurs frequently, it means that two or more concurrent transactions are waiting for one another to give up locks. A fundamental solution is to modify the SQL running logic order and optimize the locking mechanism to reduce the probability of deadlock. A temporary solution is to kill the head blocker.

#### Lock wait diagnosis
Reports lock waits lasting over 60 seconds in the current time period.

>?Lock waits are normal, but sometimes your business may display lock wait timeout errors such as `Lock wait timeout exceeded;try restarting transaction`. MySQL's InnoDB lock information is saved in tables `innodb_trx`, `innodb_lock_waits`, and `innodb_locks` in the system database `information_schema`. Lock wait diagnosis analyzes the lock dependencies in the three tables in the instance, finds the head blocker (session or transaction) that holds a lock for longer than the specified time and blocks other sessions or transactions, and then kill it.

>!Currently, lock waits are supported only by InnoDB.

#### Long running session diagnosis
Lists the sessions whose `Command` column is not `Sleep` but execution time exceeds 10 seconds by diagnosing the `information_schema.processlist` table in the instance.

>?The best solution to long running sessions is to optimize SQL and proactively place session invalidation configuration in your business code. Of course, you can also make expired sessions automatically invalid by adjusting the `interactive_timeout` and `wait_timeout` parameters.


#### Slow query analysis
Lists the current top 20 slow query statements based on the number of executions in reverse order.

>?The slow query threshold can be adjusted by the `long_query_time` parameter. Slow queries may occur for many reasons. Generally, if your instance consumes reasonable amounts of resources but a lot of slow queries occur, you are recommended to check whether your business SQL and indexes are appropriate. If your instance has high performance overhead and a lot of slow queries occur, you are recommended to check whether your instance configuration is appropriate and optimize your business SQL and indexes. You can query more details of slow queries using the slow query analysis feature.

#### Database status check
Checks the health of databases in the current instance.

#### Others
Lists other values that require DBA's attention.

