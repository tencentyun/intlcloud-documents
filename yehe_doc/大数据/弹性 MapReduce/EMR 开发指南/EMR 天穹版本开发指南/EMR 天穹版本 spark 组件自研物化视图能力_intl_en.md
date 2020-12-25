Materialized views are mainly used to perform precomputation and save the results of time-consuming operations such as table joins or aggregations. When a query task is being executed, the time-consuming operations are skipped so that you get the result quickly. Materialized views use a query rewrite mechanism, which selects the appropriate materialized view to query without the need to modify the original query statement. In addition, query rewrite is transparent to applications.
Use limits on materialized views:
- Cannot create materialized views with subqueries.
- Cannot create materialized views with UNION statements.

This document provides detailed information about the creation and management of materialized views in Spark SQL, and describes the applicable scope and use limits of the rewrite algorithm via examples.
## Creating a Materialized View


```
CREATE MATERIALIZED VIEW [IF NOT EXISTS] [db_name.]materialized_view_name
[DISABLE REWRITE]
[COMMENT materialized_view_comment]
[PARTITIONED ON (col_name, ...)]
[CLUSTERED ON (col_name, ...) | DISTRIBUTED ON (col_name, ...) SORTED ON (col_name, ...)]
[
[ROW FORMAT row_format]
[STORED AS file_format]
| STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]
]
[LOCATION hdfs_path]
[TBLPROPERTIES (property_name=property_value, ...)]
AS
<query>;
```
>?
>- Please do not use the `DISABLE REWRITE` option, otherwise you will not be able to use the materialized view feature. Set `$db_name` to `mv_db`, otherwise you will need to change the `spark.sql.materializedView.databases` parameter to `$db_name`.
>- Please create an independent mv_db to store materialized views. This can improve the efficiency of matching materialized views and obtaining metadata.

## Materialized View Samples
1. Preparing basic data
```
CREATE DATABASE  mv_database location "/mv";
use mv_database;
create external table if not exists mv_database.table1 (id int,name string) ;
create external table if not exists mv_database.table2 (id int, tags string);
insert into  table1  values (1,'1111'),(2,'2222') ;
insert into table1 values (123,'123123'),(678,'678678');
insert into table2 values (1,'iam1'),(2,'iam2'),(123,'iam123'),(678,'iam678');
```
2. Creating a materialized view
```
$spark-sql --database mv_database --master yarn
spark-sql> set spark.sql.materializedView.enable=true;
spark-sql>set spark.sql.materializedView.databases=mv_db;
spark-sql> create materialized view mv_db.mv_test_join
as
select t1.id,t1.name,t2.tags
from mv_database.table1 t1 join
mv_database.table2 t2
where
t1.id=t2.id;
```
3. Testing a materialized view

```
spark-sql> explain extended select t1.id,t1.name,t2.tags
         > from mv_database.table1 t1 join
         > mv_database.table2 t2
         > where
         > t1.id=t2.id;
== Parsed Logical Plan ==
'Project ['t1.id, 't1.name, 't2.tags]
+- 'Filter ('t1.id = 't2.id)
   +- 'Join Inner
      :- 'SubqueryAlias t1
      :  +- 'UnresolvedRelation [mv_database, table1]
      +- 'SubqueryAlias t2
         +- 'UnresolvedRelation [mv_database, table2]
== Analyzed Logical Plan ==
id: int, name: string, tags: string
Project [id#26, name#27, tags#29]
+- Filter (id#26 = id#28)
   +- Join Inner
      :- SubqueryAlias t1
      :  +- SubqueryAlias spark_catalog.mv_database.table1
      :     +- HiveTableRelation `mv_database`.`table1`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#26, name#27]
      +- SubqueryAlias t2
         +- SubqueryAlias spark_catalog.mv_database.table2
            +- HiveTableRelation `mv_database`.`table2`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#28, tags#29]
== Materialized Logical Plan ==
Project [id#40 AS id#26, name#41 AS name#27, tags#42 AS tags#29]
+- SubqueryAlias spark_catalog.mv_db.mv_test_join
   +- HiveTableRelation `mv_db`.`mv_test_join`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#40, name#41, tags#42]
== Optimized Logical Plan ==
HiveTableRelation `mv_db`.`mv_test_join`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#40, name#41, tags#42]
== Physical Plan ==
Scan hive mv_db.mv_test_join [id#40, name#41, tags#42], HiveTableRelation `mv_db`.`mv_test_join`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#40, name#41, tags#42]
```
The following codes indicate that the created materialized view is hit and the logical plan is rewritten for better performance.
```
== Materialized Logical Plan ==
Project [id#40 AS id#26, name#41 AS name#27, tags#42 AS tags#29]
+- SubqueryAlias spark_catalog.mv_db.mv_test_join
   +- HiveTableRelation `mv_db`.`mv_test_join`, org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe, [id#40, name#41, tags#42]
```

## Matching Policy of Materialized Views
Materialized views of TianQiong-Spark use the one-hit policy by default. You can adjust their matching policy by setting the following parameters:
```
spark.sql.materializedView.matchPolicy
spark.sql.materializedView.multiplePolicy.limit
```
For example, if you want to use a policy of up to five hits, set the `session` parameter of `spark-sql` as follows:
```
spark-sql>set spark.sql.materializedView.matchPolicy=multiple;
spark-sql>set spark.sql.materializedView.multiplePolicy.limit=5;
```


## Recreating a Materialized View
When the data in the source table used by a materialized view changes, for example, new data is inserted or existing data is modified, you need to refresh the content of the materialized view to keep it up to date. Currently, users need to trigger the recreation of materialized views by executing the following statement:
```
ALTER MATERIALIZED VIEW [db_name.]materialized_view_name REBUILD;
```

## Rewriting a Materialized View
Once a materialized view is created, the optimizer will be able to utilize its definition semantics to automatically rewrite incoming queries using the materialized view, and hence accelerate query execution.

You can enable or disable materialized views for rewriting. By default, materialized views are enabled when they are created. You can disable this feature by executing the following statement:
```
ALTER MATERIALIZED VIEW [db_name.]materialized_view_name enable|disable REWRITE;
```

## Deleting a Materialized View and Performing Other Operations
Currently we support the following operations on materialized views:
1. Delete a materialized view.
```
DROP MATERIALIZED VIEW [db_name.]materialized_view_name;
```
2. Show materialized views.
```
SHOW MATERIALIZED VIEWS [IN database_name] ['identifier_with_wildcards’];
```
3. Show the information about a specific materialized view.
```
DESCRIBE [EXTENDED | FORMATTED] [db_name.]materialized_view_name;
```
