It collects statistics about a database.

## Synopsis
```sql
ANALYZE [VERBOSE] [ROOTPARTITION [ALL] ] 
   [table [ (column [, ...] ) ]]
```

## Description
`ANALYZE` collects statistics about the contents of tables in the database, and stores the results in the `pg_statistic` system catalog. Subsequently, the query planner uses these statistics to help determine the most efficient execution plans for queries.

With no parameter, `ANALYZE` collects statistics for every table in the current database. You can specify a table name to collect statistics for a single table. You can specify a set of column names, in which case the statistics only for those columns are collected.

`ANALYZE` does not collect statistics on external tables.

**If you intend to execute queries on partitioned tables with GPORCA enabled (the default), then you must collect statistics on the root partition of the partitioned table with the `ANALYZE ROOTPARTITION` command. For information about GPORCA, see "Data Query" in the Database Administrator Guide.**

>! You can also use the database utility `analyzedb` to update table statistics. The `analyzedb` utility can update statistics for multiple tables concurrently. The utility can also check table statistics and update statistics only if the statistics are not current or do not exist. For information about the utility, see the Database Utility Guide.

## Parameters
ROOTPARTITION [ALL]
Statistics are collected only on the root partition of the partitioned table. Statistics are not collected on the leaf child partitions, the data is only sampled. When you specify ROOTPARTITION, you must specify either ALL or the name of a partitioned table.

If you specify `ALL` with `ROOTPARTITION`, the database collects statistics for the root partition of all partitioned tables in the database. If there are no partitioned tables in the database, a message stating that there are no partitioned tables is returned. For tables that are not partitioned tables, statistics are not collected.

If you specify a table name with `ROOTPARTITION` and the table is not a partitioned table, no statistics are collected for the table and a warning message is returned.

The `ROOTPARTITION` clause is not valid with `VACUUM ANALYZE`. The command `VACUUM ANALYZE ROOTPARTITION` returns an error.

The time to run `ANALYZE ROOTPARTITION` is similar to the time to analyze a non-partitioned table with the same data since `ANALYZE ROOTPARTITION` only samples the leaf child partition data.

For the partitioned table `sales_curr_yr`, this example command collects statistics only on the root partition of the partitioned table.

ANALYZE ROOTPARTITION sales_curr_yr
This example `ANALYZE` command collects statistics on the root partition of all the partitioned tables in the database.
```sql
ANALYZE ROOTPARTITION ALL;
```
VERBOSE
Enables display of progress messages. When specified, `ANALYZE` emits this information:

- The table that is being processed.
- The query that is executed to generate the sample table.
- The column for which statistics is being computed.
- The queries that are issued to collect the different statistics for a single column.
- The statistics that are generated.

table
The name (possibly schema-qualified) of a specific table to analyze. Defaults to all tables in the current database.

column
The name of a specific column to analyze. Defaults to all columns.

## Notes
It is a good idea to run `ANALYZE` periodically, or just after making major changes in the contents of a table. Accurate statistics helps the database choose the most appropriate query plan, and thereby improves the speed of query processing. A common strategy is to run [`VACUUM`](https://gp-docs-cn.github.io/docs/ref_guide/sql_commands/VACUUM.html#topic1) and `ANALYZE` once a day during a low-usage time of day.

`ANALYZE` requires `SHARE UPDATE EXCLUSIVE` lock on the target table. This lock conflicts with these locks: `SHARE UPDATE EXCLUSIVE`, `SHARE`, `SHARE ROW EXCLUSIVE`, `EXCLUSIVE`, `ACCESS EXCLUSIVE`.

For a partitioned table, specifying which portion of the table to analyze, the root partition or subpartitions (leaf child tables) can be useful if the partitioned table has a large number of partitions that have been analyzed and only a few leaf child partitions have changed.

- When you run `ANALYZE` on the root partitioned table, statistics are collected for all the leaf child partitions. Leaf child partitions are the lowest-level tables in the hierarchy of child tables created by the database for use by the partitioned table.
- When you run `ANALYZE` on a leaf child partition, statistics are collected only for that leaf child partition. When you run `ANALYZE` on a child table that is not a leaf child partition, statistics are not collected.

For example, you can create a partitioned table with partitions for the years 2006 to 2016 and subpartitions for each month in each year. If you run `ANALYZE` on the child table for the year 2013 no statistics are collected. If you run `ANALYZE` on the leaf child partition for March of 2013, statistics are collected only for that leaf child partition.

>!When you create a partitioned table with the `CREATE TABLE` command, the database creates the table that you specify (the root partition or parent table), and also creates a hierarchy of tables based on the partition hierarchy that you specified (the child tables). Partitioned tables, child tables, and their inheritance hierarchies are tracked through the system view `pg_partitions`.

For a partitioned table that contains a leaf child partition that has been exchanged to use an external table, `ANALYZE` does not collect statistics for the external table partition:
- If `ANALYZE [ROOTPARTITION]` is run, external tables are not sampled and root table statistics do not include external table partitions.
- If `ANALYZE` is run on an external table partition, the partition is not analyzed.
- If the `VERBOSE` clause is specified, an informational message is displayed: skipping external table.

The database server configuration parameter `optimizer_analyze_root_partition` affects when statistics are collected on the root partition of a partitioned table. If the parameter is on, statistics are collected for the root partition when you run `ANALYZE` (without the `ROOTPARTITON` keyword) and specify the root partition.

The statistics collected by `ANALYZE` usually include a list of some of the most common values in each column and a histogram showing the approximate data distribution in each column. One or both of these may be omitted if `ANALYZE` deems them uninteresting (for example, in a unique-key column, there are no common values) or if the column data type does not support the appropriate operators.

For large tables, `ANALYZE` takes a random sample of the table contents, rather than examining every row. This allows even very large tables to be analyzed in a small amount of time. Note, however, that the statistics are only approximate, and will change slightly each time `ANALYZE` is run, even if the actual table contents did not change. This may result in small changes in the planner's estimated costs shown by `EXPLAIN`. In rare situations, this non-determinism will cause the query optimizer to choose a different query plan between runs of `ANALYZE`.

To avoid this, raise the amount of statistics collected by `ANALYZE` by adjusting the `default_statistics_target` configuration parameter, or on a column-by-column basis by setting the per-column statistics target with ALTER TABLE ... ALTER COLUMN ... SET STATISTICS (see `ALTER TABLE`). The target value sets the maximum number of entries in the most-common-value list and the maximum number of bins in the histogram. The default target value is 10, but this can be adjusted up or down to trade off accuracy of planner estimates against the time taken for `ANALYZE` and the amount of space occupied in `pg_statistic`. In particular, setting the statistics target to zero disables collection of statistics for that column. It may be useful to do that for columns that are never used as part of the `WHERE`, `GROUP BY`, or `ORDER BY` clauses of queries, since the planner will have no use for statistics on such columns.

The largest statistics target among the columns being analyzed determines the number of table rows sampled to prepare the statistics. Increasing the target causes a proportional increase in the time and space needed to do `ANALYZE`.

When the database performs an `ANALYZE` operation to collect statistics for a table and detects that all the sampled table data pages are empty (do not contain valid data), the database displays a message that a `VACUUM FULL` operation should be performed. If the sampled pages are empty, the table statistics will be inaccurate. Pages become empty after a large number of changes to the table, for example deleting a large number of rows. A `VACUUM FULL` operation removes the empty pages and allows an `ANALYZE` operation to collect accurate statistics.

If there are no statistics for the table, the server configuration parameter `gp_enable_relsize_collection` controls whether the legacy query optimizer uses a default statistics file or estimates the size of a table using the `pg_relation_size` function. By default, the legacy optimizer uses the default statistics file to estimate the number of rows if statistics are not available.

## Examples
Collect statistics for the table `mytable`:
```sql
ANALYZE mytable;
```

## Compatibility
There is no `ANALYZE` statement in the SQL standard.

## See Also
ALTER TABLE, EXPLAIN, VACUUM
