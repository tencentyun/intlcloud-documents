## Creating a Database
Initially, you can create a database through the root or admin account with the following command:
```
CREATE DATABASE example_db;
```
All commands can use `HELP command` to see detailed syntax help. For example: `HELP CREATE DATABASE;`.

If you don't know the full name of the command, you can use "help + a field" for fuzzy query. For example, if you type `HELP CREATE`, you can get commands like `CREATE DATABASE`, `CREATE TABLE`, and `CREATE USER`.

After the database is created, you can view the database information through `SHOW DATABASES;`.
```
MySQL> SHOW DATABASES;
+--------------------+
| Database      |
+--------------------+
| example_db     |
| information_schema |
+--------------------+
2 rows in set (0.00 sec)
```
`information_schema` exists to be compatible with the MySQL protocol. In practice, information may not be accurate. Therefore, you are advised to obtain the information about specific databases by directly querying the corresponding databases.

## Account Authorization
After the `example_db` database is created, you can authorize the read/write permissions for `example_db` to an ordinary account, such as test, through the root or admin account. After authorization, you can log in to and operate `example_db` using the test account.
```
GRANT ALL ON example_db TO test;
```

### Creating a table
Create a table with the `CREATE TABLE` command. More parameter information can be seen by running the `HELP CREATE TABLE;` command.

Switch the database using the following command:
```
USE example_db;
```
Doris supports two ways to create a table: single partitioning and composite partitioning.

In composite partitioning:
- The first level is called Partition, or partitioning. Users can specify a dimension column as a partition column (currently only integer and time columns are supported), and specify the value range for each partition.
- The second level is called Distribution, or bucketing. Users can specify one or more dimension columns and the number of buckets for HASH distribution of data.

Composite partitioning is recommended for the following scenarios:
- There are time dimensions or similar dimensions with ordered values, which can be used as partition columns. The partition granularity can be evaluated according to the frequency of import and the amount of partition data.
- Historical data deletion requirements: for example, only to retain the data of the last N days. Using composite partitioning, you can achieve this by deleting historical partitions. You can also delete data by sending a `DELETE` statement within a specified partition.
- Solving the data skew issue: you can specify the number of buckets for each partition separately. For partitioning by day, when the amount of data varies greatly every day, you can divide the data of different partitions by specifying the number of buckets in the partitions. You are advised to choose columns with high differentiation as the bucket columns.
- You can use single partitioning instead of composite partitioning. Then the data are only distributed by HASH.

The following takes the aggregation model as an example to separately illustrate the table creation statements of the two kinds of partitioning.

### Single partitioning
Create a logical table named `table1`. The bucket column is `siteid` and the number of buckets is 10. The schema of this table is as follows:
- `siteid`: the type is `INT` (4 bytes); the default value is `10`.
- `citycode`: the type is `SMALLINT` (2 bytes).
- `username`: the type is `VARCHAR`; the maximum length is `32`; the default value is an empty string.
- `pv`: the type is `BIGINT` (8 bytes); the default value is `0`. This is a metric column. Doris will aggregate the metric column internally. The aggregation method of this column is `SUM`.

The table creation statement is as follows:
```
CREATE TABLE table1
(
		siteid INT DEFAULT '10',
		citycode SMALLINT,
		username VARCHAR(32) DEFAULT '',
		pv BIGINT SUM DEFAULT '0'
)
AGGREGATE KEY(siteid, citycode, username)
DISTRIBUTED BY HASH(siteid) BUCKETS 10
PROPERTIES("replication_num" = "1");
```

### Composite partitioning
Create a logical table named `table2`. The schema of this table is as follows:
- `event_day`: the type is `DATE`; no default value.
- `siteid`: the type is `INT` (4 bytes); the default value is `10`.
- `citycode`: the type is `SMALLINT` (2 bytes).
- `username`: the type is `VARCHAR`; the maximum length is `32`; the default value is an empty string.
- `pv`: the type is `BIGINT` (8 bytes); the default value is `0`. This is a metric column. Doris will aggregate the metric column internally. The aggregation method of this column is `SUM`.

The `event_day` column is used as the partition column to create three partitions: `p201706`, `p201707`, and `p201708`.
- `p201706`: the range is [Minimum, 2017-07-01).
- `p201707`: the range is [2017-07-01, 2017-08-01).
- `p201708`: the range is [2017-08-01, 2017-09-01).

>!Note that the interval is left-closed and right-open.

Each partition uses `siteid` to hash buckets, with a bucket count of 10. The table creation statement is as follows:
```
CREATE TABLE table2
(
			event_day DATE,
			siteid INT DEFAULT '10',
			citycode SMALLINT,
			username VARCHAR(32) DEFAULT '',
			pv BIGINT SUM DEFAULT '0'
)
AGGREGATE KEY(event_day, siteid, citycode, username)
PARTITION BY RANGE(event_day)
(
			PARTITION p201706 VALUES LESS THAN ('2017-07-01'),
			PARTITION p201707 VALUES LESS THAN ('2017-08-01'),
			PARTITION p201708 VALUES LESS THAN ('2017-09-01')
)
DISTRIBUTED BY HASH(siteid) BUCKETS 10
PROPERTIES("replication_num" = "1");
```
After the table is created, you can view the information of the table in `example_db`:
```
MySQL> SHOW TABLES;

+----------------------+
| Tables_in_example_db |
+----------------------+
| table1        |
| table2        |
+----------------------+
2 rows in set (0.01 sec)


MySQL> DESC table1;

+----------+-------------+------+-------+---------+-------+
| Field  | Type    | Null | Key  | Default | Extra |
+----------+-------------+------+-------+---------+-------+
| siteid  | int(11)   | Yes | true | 10   |    |
| citycode | smallint(6) | Yes | true | N/A   |    |
| username | varchar(32) | Yes | true |     |    |
| pv    | bigint(20) | Yes | false | 0    | SUM  |
+----------+-------------+------+-------+---------+-------+
4 rows in set (0.00 sec)


MySQL> DESC table2;

+-----------+-------------+------+-------+---------+-------+
| Field   | Type    | Null | Key  | Default | Extra |
+-----------+-------------+------+-------+---------+-------+
| event_day | date    | Yes | true | N/A   |    |
| siteid  | int(11)   | Yes | true | 10   |    |
| citycode | smallint(6) | Yes | true | N/A   |    |
| username | varchar(32) | Yes | true |     |    |
| pv    | bigint(20) | Yes | false | 0    | SUM  |
+-----------+-------------+------+-------+---------+-------+

5 rows in set (0.00 sec)
```

### Notes
>?For more syntax description regarding the use of Doris, see [Data Table Creation and Data Import](https://doris.incubator.apache.org/getting-started/basic-usage.html#_2-data-table-creation-and-data-import).

1. The above tables created by setting `replication_num` are all single-replica tables. Doris recommends that users adopt the default three-replica settings to ensure high availability.
2. Partitions in composite partitioning tables can be added or deleted dynamically.
3. Data can be imported by importing a specified partition.
4. The schema of table can be dynamically modified.
5. Rollup can be added to a table to improve the query performance.
6. The default value of the `Null` attribute for column is `true`, which may affect the query performance.

## Importing Data
Doris supports a variety of data import methods. The following uses streaming import and broker import as examples.

### Streaming import
Streaming import transfers data to Doris over the HTTP protocol. It can import local data directly without relying on other systems or components.

#### Example 1
With `table1_20170707` as the label, import the `table1` table using the `table1_data` local file.
```
curl --location-trusted -u test:test -H "label:table1_20170707" -H "column_separator:," -T table1_data http://FE_HOST:8030/api/example_db/table1/_stream_load
```
1. `FE_HOST` is the IP of any FE node and `8030` is the `http_port` in `fe.conf`.
2. You can use the IP of any BE and the `webserver_port` in `be.conf` for import. For example: `BE_HOST:8040`.

The `table1_data` local file uses a comma (,) as the separator between data. The specific content is as follows:
```
1,1,jim,2
2,1,grace,2
3,2,tom,2
4,3,bush,3
5,3,helen,3
```

#### Example 2
With `table2_20170707` as the label, import the `table2` table using the `table2_data` local file.
```
curl --location-trusted -u test:test -H "label:table2_20170707" -H "column_separator:|" -T table2_data http://127.0.0.1:8030/api/example_db/table2/_stream_load
```
The `table2_data` local file uses a vertical bar (|) as the separator between data. The specific content is as follows:
```
2017-07-03|1|1|jim|2
2017-07-05|2|1|grace|2
2017-07-12|3|2|tom|2
2017-07-15|4|3|bush|3
2017-07-12|5|3|helen|3
```

#### Precautions
1. The recommended file size for streaming imports is no greater than 10 GB. Excessive file size will result in failure and increase the costs of retry.
2. Each batch of imported data needs to take a label. The label is preferably a string related to the batch of data for easy reading and management. Doris guarantees that the same batch of data can be imported only once in a database based on label. Labels for failed tasks can be reused.
3. Streaming imports are synchronous commands. The successful return of the command indicates that the data has been imported, and the failed return indicates that the data has not been imported.

### Broker import
Broker imports import data from external storage through deployed broker processes.

With `table1_20170708` as the label, import files on HDFS into the `table1` table.
```
LOAD LABEL table1_20170708
(
			DATA INFILE("hdfs://your.namenode.host:port/dir/table1_data")
			INTO TABLE table1
)

WITH BROKER hdfs 
(
			"username"="hdfs_user",
			"password"="hdfs_password"
)

PROPERTIES
(
			"timeout"="3600",
			"max_filter_ratio"="0.1"
);
```
Broker imports are asynchronous commands. Successful execution of the above commands only indicates successful submission of tasks. Successful imports need to be checked through `SHOW LOAD;'. The command is as follows:
```
SHOW LOAD WHERE LABEL = "table1_20170708";
```
In the return result, `FINISHED` in the `State` field indicates that the import was successful.

Asynchronous import tasks can be canceled before the end by using the following command:
```
CANCEL LOAD WHERE LABEL = "table1_20170708";
```

 
