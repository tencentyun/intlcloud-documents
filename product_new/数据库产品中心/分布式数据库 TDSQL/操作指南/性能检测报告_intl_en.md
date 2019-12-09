## Overview
Performance test is a comprehensive analysis service for database instance performance and health. It can analyze SQL statement performance, CPU utilization, IOPS utilization, memory utilization, disk utilization, connections, locks, hotspot tables, and transactions, helping you identify and address existing and potential health issues in your database through smart diagnosis and optimization.

This feature is currently available in the following instance editions:
- TDSQL
- TencentDB for MariaDB

>For certain test items, the performance test report provides a series of optimization suggestions. Please carefully test the suggested measures before applying them so as to prevent the instance performance problems from getting worse.

## Features
- **Health rating:** You can view the current database performance score out of 100 points. If your database scores below 60 for a long time, please optimize your business or database configuration.
- **Report generation, viewing, and saving:** You can create a report or view the last report as desired. The report can be saved as a webpage for downloaded.

## Main test items

#### Resource analysis
Analyzes the usage of database instance resources (CPU, disk, and connections) in a certain period of time and displays an overall score.

>As most instances have an "overuse when idle" policy enabled by default, you may observe that the maximum CPU utilization exceeds 100%. If this is persistent and the average is higher than the recommended value, you are recommended to scale your instance up.

#### System status
Sorts out key instance metrics, lists their status and time of occurrence, and suggests corresponding modifications.

#### Table space distribution
Lists the current top 10 tables in reverse order in terms of data space to help you identify oversized tables.

#### Redundant index detection
Lists the current possible redundant indices (with redundancy discrimination below 1%) and suggests optimizations.

>Because a query statement must first query the indices before querying tables through indices, if there are too many identical data entries in the index column, the performance to reduce the amount of data to be filtered may be compromised and is not as fast as full table scan.

#### Deadlock diagnosis
The deadlock diagnosis gets the information of the last deadlock in the database through `show engine innodb status` and displays it if the deadlock occurs within the selected diagnostic time period.

>If deadlock occurs frequently, it means that the SQL in the transactions is prone to generate locking loops in concurrent execution scenarios. A fundamental solution is to modify the SQL running logic order and optimize the locking mechanism to reduce the probability of deadlock. A temporary solution is to kill the blocking session leader.

#### Lock wait diagnosis
Reports lock waits lasting over 60 seconds in the current time period.

>
>- Lock waits are normal, but sometimes your business may display lock wait timeout errors such as `Lock wait timeout exceeded;try restarting transaction`. MySQL's InnoDB lock information is saved in tables `innodb_trx, innodb_lock_waits, innodb_locks` in `information_schema`. Lock wait diagnosis analyzes the lock dependencies in the three tables in the set's master DB, finds the session leader that holds a lock for longer than the specified time and blocks other sessions, and then kills it.
>- Current, lock wait is only supported for the InnoDB engine.

#### Long session diagnosis
Lists the sessions whose command is not "sleep" but execution time exceeds 10 seconds by diagnosing `information_schema.processlist` in the set's master DB.

>The best solution to long sessions is to optimize SQL and proactively place session invalidation configuration in your business code. Of course, you can also make expired sessions automatically invalid by adjusting the `interactive_timeout` and `wait_timeout` parameters.


#### Slow log analysis
Lists the current top 20 slow log statements based on the number of executions in reverse order.

>The slow log threshold can be adjusted in the `long_query_time` parameter. Slow logs may occur for many reasons. Generally, if your instance consumes reasonable amounts of resources but a lot of slow logs occur, you are recommended to check whether your business SQL and indices are appropriate. If your instance has high performance overhead and a lot of slow logs occur, you are recommended to check whether your instance configuration is appropriate and optimize your business SQL and indices. You can query more details of slow logs using the slow log analysis feature.

#### DB status check
Checks the health status of the DB layer in the current database.

#### Other
Lists other values that require DBA's attention.

