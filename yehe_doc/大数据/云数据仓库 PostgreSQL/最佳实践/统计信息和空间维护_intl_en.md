## Background
Cluster statistics are critical to the use of clusters, and CDWPG's query optimizer is based on the dynamically calculated cost to determine how to make selections. How is the cost calculated? Usually, the calculation is based on the cost model and statistics. The cost model reasonableness and statistics accuracy will affect the effectiveness of query optimization.

The utilization of cluster tablespaces also affects the query cost. When a table has `UPDATE` operations (including `INSERT VALUES`, `UPDATE`, `DELETE`, `ALTER TABLE`, and `ADD COLUMN`), it will leave garbage data that is no longer used in the system table and the updated table, causing system performance degradation and taking up a lot of disk space. Therefore, you need to regularly monitor the data bloat of the table.

The following details the regular monitoring and maintenance of statistics and data bloat.

## Statistics Collection
`ANALYZE` collects table statistics in a database and stores the results in the `pg_statistic` system directory. The query planner uses such statistics to help determine the most efficient execution plan for a query. The statistics contain various information such as the amount of data and indexes in the table. A good query plan is based on accurate table statistics.

### `ANALYZE` description
`ANALYZE` is a command provided by Greenplum to collect statistics and supports column, table, and database granularities as shown below:
```
CREATE TABLE foo (id int NOT NULL, bar text NOT NULL) DISTRIBUTED BY (id); // Create the test table `foo`
ANALYZE foo(bar);  // Collect statistics of the `bar` column only
ANALYZE foo; // Collect statistics of the `foo` table
ANALYZE; // Collect statistics of all tables in the current database. You need to have the permission to do so
```

### Use limits of `ANALYZE`
`ANALYZE` will put a `SHARE UPDATE EXCLUSIVE` lock on the target table, which will conflict with DDL statements.

### `ANALYZE` speed
`ANALYZE` is a sampling statistical algorithm that usually does not scan all data in a table, but still consumes some time and computing resources for large tables.

### Time to use `ANALYZE`
As mentioned above, `ANALYZE` locks tables and consumes system resources, so it is important to run it at the right time and as little as possible. We recommend you run `ANALYZE` in the following four scenarios.
- After data is batch loaded; for example, after data is imported to a newly created table.
- After an index is created.
- After `INSERT`, `UPDATE`, and `DELETE` operations are performed on a large amount of data.
- After `VACUUM FULL` is executed.

### Analyzing partitioned table
As long as you keep the default value and do not modify the system parameter `optimizer_analyze_root_partition`, there is no difference in manipulating a partitioned table. Just run `ANALYZE` on the root table, and the system will automatically collect the statistics of partitioned tables on all leaf nodes.

If the number of partitioned tables is high, running `ANALYZE` on the root table can be time-consuming. Partitioned tables are usually time-dimensional, and historical partitioned tables are not modified; therefore, we recommend you run `ANALYZE` separately in partitions where data changes.

## Data Bloat
The Greenplum database's heap table uses PostgreSQL's multiple version concurrency control (MVCC) storage implementation. The database will logically delete a deleted or updated row, but an invisible image of that row will remain in the table. As more operations are performed, the table will have more and more invisible data, which will take up a lot of storage space, thereby causing a serious performance degradation in table operations. Additionally, the data bloat can occupy a lot of space, which needs to be regularly fixed.

### Data bloat monitoring
The `gp_toolkit` schema provides a `gp_bloat_diag` view that determines the table bloat by the ratio of the actual number of pages to the expected number of pages. To use this view, make sure that the latest statistics are collected for all tables in the database. Then, run the following SQL:
```
gpadmin=# SELECT * FROM gp_toolkit.gp_bloat_diag;
 bdirelid | bdinspname | bdirelname | bdirelpages | bdiexppages |                bdidiag                
----------+------------+------------+-------------+-------------+---------------------------------------
    21488 | public     | t1         |          97 |           1 | significant amount of bloat suspected
(1 row)
```
Here, `bdirelpage` is the actual number of pages and `bdiexppages` is the expected number of pages in the `t1` table. A bloat ratio exceeding 4 will be recorded in the table, and there may also be a slight bloat even when no ratio is recorded. You can also compare the space of tables at different times to determine whether data has bloated.

### Cleaning data bloat in table

The `VACUUM <tablename>` command adds expired rows to the shared free space map, so such space can be reused. When `VACUUM` is run periodically on a table with frequent `UPDATE` operations, the space occupied by expired rows can be reused quickly, easing table bloat. The cycle to run `VACUUM` is determined by the speed of `UPDATE` and `DELETE` on the table.
>!`VACUUM` holds a `SHARE UPDATE EXCLUSIVE` lock as `ANALYZE` does and may interlock with DDL operations.

When the table experiences a significant bloat, `VACUUM` can only slow down the process but not immediately reclaim the space. Therefore, you need to run `VACUUM FULL` to immediately reclaim all the bloat space. However, `VACUUM FULL` will add `ACCESS EXCLUSIVE` to the manipulated table, during which all other DDL and DML statements on the table will be locked. Proceed with caution when running `VACUUM FULL` as the operation may be time-consuming for large tables.

Another way to address bloat is to redistribute data in the table:
1. Record the distribution key of the table.
2. Change the distribution policy of the table to random distribution.
```
ALTER TABLE <tablename> SET WITH (REORGANIZE=false) 
                DISTRIBUTED randomly;
```
3. Change the distribution policy back to the initial one.
```
ALTER TABLE <table_name> SET WITH (REORGANIZE=true) 
DISTRIBUTED BY (<original distribution columns>);
```

### Handling index bloat
The `VACUUM FULL` command will only reclaim spaces from tables. To reclaim spaces from indexes, you need to rebuild them with the `REINDEX` command.
```
REINDEX TABLE <table_name>    --- Rebuild all indexes in the table  
REINDEX INDEX <index_name> --- Rebuild a specified index
```
>!Note that both `REINDEX` and `VACUUM FULL` will add `ACCESS EXCLUSIVE`.

## Regular Cluster Maintenance
When using a cluster, you need to eliminate data bloat and maintain statistics regularly so that the cluster can deliver an optimal performance.

### Cleaning without table locking
As mentioned above, `VACUUM <tablename>` can mark reclaimable space without table locking and slow down data bloat. Cleaning without locking the table will not affect data table reads/writes, but DDL statements cannot be used, and some CPU and memory resources will be used.

**Recommended frequency:**
- Once a day or at least twice a week if a large amount of data is updated in real time and many data records change every day.
- Once a week under normal circumstances or once a month if data is not updated frequently.

Use the following script to clean a table with a cron job.
```
#!/bin/bash
export PGHOST=xxx.xxx.x.x
export PGPORT=5436
export PGUSER=test
export PGPASSWORD=test
db="test"
psql -d $db -e -c "VACUUM test_table;"
```

### Full cleaning with table locking
If the data in a table is updated and deleted frequently, we recommend you plan a business pause window to run `VACUUM FULL` and `REINDEX` to reclaim all the bloat space in the table. Cleaning with table locking will put an `ACCESS EXCLUSIVE` lock on the manipulated table, during which you cannot perform any operations on the table.

1. Run `VACUUM FULL <tablename>`. 
2. Run `REINDEX TABLE <tablename>` (you can skip this step for tables without indexes).  
3. Run `ANALYZE <tablename> `.

**Recommended frequency:** Once a week or once a day if almost all data is updated daily.

Use the following script to regularly clean cluster tables, preferably during off hours in the early morning on the weekend.
```
#!/bin/bash
export PGHOST=xxx.xxx.x.x
export PGPORT=5436
export PGUSER=test
export PGPASSWORD=test
db="test"
psql -d $db -e -c "VACUUM FULL test_table;"
psql -d $db -e -c "REINDEX TABLE test_table;"
psql -d $db -e -c "ANALYZE test_table;"
```
