Currently, StarRocks can be connected to in different ways. This document describes how to use a MySQL client to connect to StarRocks for development.

## Logging in as Root User
Use the MySQL client to connect to the query port (9030) of an FE instance. StarRocks is preconfigured with the root user, whose password is the cluster password:
```shell
mysql -h fe_host -P9030 -u root -p
```
Clean up the environment:
```sql
mysql > drop database if exists example_db;

mysql > drop user test;
```

## Viewing Deployed Nodes
1. View the FE node.
```
mysql> SHOW PROC '/frontends'\G

************************* 1. row ************************
             Name: 172.16.139.24_9010_1594200991015
               IP: 172.16.139.24
         HostName: starrocks-sandbox01
      EditLogPort: 9010
         HttpPort: 8030
        QueryPort: 9030
          RpcPort: 9020
             Role: FOLLOWER
         IsMaster: true
        ClusterId: 861797858
             Join: true
            Alive: true
ReplayedJournalId: 64
    LastHeartbeat: 2020-03-23 20:15:07
         IsHelper: true
           ErrMsg:
1 row in set (0.03 sec)
```
The value of `Role` is `FOLLOWER`, indicating that the FE is eligible for master election. The value of `IsMaster` is `true`, indicating that the FE is the current master node.


2. Viewing the BE node.
```
mysql> SHOW PROC '/backends'\G

********************* 1. row **********************
            BackendId: 10002
              Cluster: default_cluster
                   IP: 172.16.139.24
             HostName: starrocks-sandbox01
        HeartbeatPort: 9050
               BePort: 9060
             HttpPort: 8040
             BrpcPort: 8060
        LastStartTime: 2020-03-23 20:19:07
        LastHeartbeat: 2020-03-23 20:34:49
                Alive: true
 SystemDecommissioned: false
ClusterDecommissioned: false
            TabletNum: 0
     DataUsedCapacity: .000
        AvailCapacity: 327.292 GB
        TotalCapacity: 450.905 GB
              UsedPct: 27.41 %
       MaxDiskUsedPct: 27.41 %
               ErrMsg:
              Version:
1 row in set (0.01 sec)
```
If the value of `isAlive` is `true`, the BE is connected to the cluster normally; if not, view the `be.WARNING` log file in the `log` directory to identify the cause.


3. View the broker node.
```
MySQL> SHOW PROC "/brokers"\G
*************************** 1. row ***************************
          Name: broker1
            IP: 172.16.139.24
          Port: 8000
         Alive: true
 LastStartTime: 2020-04-01 19:08:35
LastUpdateTime: 2020-04-01 19:08:45
        ErrMsg: 
1 row in set (0.00 sec)
```
If the value of `Alive` is `true`, the status is normal.

## Creating User
Create an ordinary user with the following command:
```sql
mysql > create user 'test' identified by '123456';
```

## Creating Database
In StarRocks, only the root account has the permission to create databases. Log in as the root user and create the `example\_db` database:
```sql
mysql > create database example_db;
```
After creating the database, you can view the database information through `show databases`:
```
mysql > show databases;

+--------------------+
| Database           |
+--------------------+
| example_db         |
| information_schema |
+--------------------+
2 rows in set (0.00 sec)
```
`information_schema` exists to be compatible with the MySQL protocol. In practice, information may not be accurate. Therefore, we recommend you get the information of a specific database by directly querying the database.

## Account Authorization
After creating the `example_db` database, you can grant its read/write permissions to the test account through the root account and then log in with the test account to manipulate the database.
```sql
mysql > grant all on example_db to test;
```
Log out of the root account and log in to the StarRocks cluster with the test account:
```sql
mysql > exit

mysql -h 127.0.0.1 -P9030 -utest -p123456
```

## Creating Table
StarRocks supports two table creation methods: single partitioning and composite partitioning.
In composite partitioning:
- The first level is called Partition, or partitioning. You can specify a dimension column as a partitioning column (currently only integer and time columns are supported) and specify the value range for each partition.
- The second level is called Distribution, i.e., bucketing. You can specify multiple dimension columns (or specify none, in which case, all `KEY` columns will be selected) and the number of buckets for HASH distribution of data.

Composite partitioning is recommended for the following scenarios:
- Scenarios involving time dimensions or similar dimensions with ordered values: You can use such dimension columns as a partitioning column and assess the partitioning granularity based on the import frequency and the amount of partitioned data.
- Historical data deletion: If you want to retain only data from the past N days, you can delete historical partitions through composite partitioning or delete data by sending a `DELETE` statement to the specified partition.
- Data skew elimination: You can specify the number of buckets for each partition separately. If you partition data by day, when the amount of data varies greatly every day, you can reasonably partition the data by specifying the number of buckets for the partitions. We recommend you select distinguishing columns as the bucket columns.

You can also use single partitioning instead of composite partitioning. Then, the data will be only distributed by HASH.
The following demonstrates the table creation statements for the two partitioning methods respectively:
1. Switch the database from `mysql` to `use example_db`.
2. Create a single-partitioned logical table named `table1` by assigning ten hash buckets based on `siteid`, with the schema as shown below:
	- `siteid`: The type is `INT` (4 bytes); the default value is `10`.
	- `city_code`: The type is `SMALLINT` (two bytes).
	- `username`: The type is `VARCHAR`. The maximum length is `32`. The default value is an empty string.
	- `pv`: The type is `BIGINT` (eight bytes), and the default value is `0`. It is a metric column and will be aggregated by StarRocks with the `SUM` method. The aggregation model is used here. In addition, StarRocks supports the detail model and update model. For more information, see [Data Model](https://docs.starrocks.com/zh-cn/main/table_design/Data_model).
The table creation statement is as follows:
```sql
mysql >
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

3. Create a composite partitioned table
Create a logical table named `table2` with the schema as shown below:
	- `event_day`: The type is `DATE`; no default value.
	- `siteid`: The type is `INT` (4 bytes); the default value is `10`.
	- `city_code`: The type is `SMALLINT` (two bytes).
	- `username`: The type is `VARCHAR`. The maximum length is `32`. The default value is an empty string.
	- `pv`: The type is `BIGINT` (eight bytes), and the default value is `0`. It is a metric column and will be aggregated by StarRocks with the `SUM` method.
Use the `event_day` column as the partitioning column to create three partitions: p1, p2, and p3.
	- p1: Its value range is \[minimum value, 2017-06-30].
	- p2: Its value range is \[2017-06-30, 2017-07-31).
	- p3: Its value range is \[2017-07-31, 2017-08-31).

 Use `siteid` to assign ten hash buckets to each partition.
The table creation statement is as follows:
```sql
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
PARTITION p1 VALUES LESS THAN ('2017-06-30'),
PARTITION p2 VALUES LESS THAN ('2017-07-31'),
PARTITION p3 VALUES LESS THAN ('2017-08-31')
)
DISTRIBUTED BY HASH(siteid) BUCKETS 10
PROPERTIES("replication_num" = "1");
```
After creating the table, you can view the information of the table in `example\_db`:
```
mysql> show tables;

+-------------------------+
| Tables_in_example_db    |
+-------------------------+
| table1                  |
| table2                  |
+-------------------------+
2 rows in set (0.01 sec)


mysql> desc table1;

+----------+-------------+------+-------+---------+-------+
| Field    | Type        | Null | Key   | Default | Extra |
+----------+-------------+------+-------+---------+-------+
| siteid   | int(11)     | Yes  | true  | 10      |       |
| citycode | smallint(6) | Yes  | true  | N/A     |       |
| username | varchar(32) | Yes  | true  |         |       |
| pv       | bigint(20)  | Yes  | false | 0       | SUM   |
+----------+-------------+------+-------+---------+-------+
4 rows in set (0.00 sec)


mysql> desc table2;

+-----------+-------------+------+-------+---------+-------+
| Field     | Type        | Null | Key   | Default | Extra |
+-----------+-------------+------+-------+---------+-------+
| event_day | date        | Yes  | true  | N/A     |       |
| siteid    | int(11)     | Yes  | true  | 10      |       |
| citycode  | smallint(6) | Yes  | true  | N/A     |       |
| username  | varchar(32) | Yes  | true  |         |       |
| pv        | bigint(20)  | Yes  | false | 0       | SUM   |
+-----------+-------------+------+-------+---------+-------+
5 rows in set (0.00 sec)
```
