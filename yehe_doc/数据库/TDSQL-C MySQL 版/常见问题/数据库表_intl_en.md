
### What are the strengths of TDSQL-C for MySQL's big table storage over traditional databases using local disks?
A table in TDSQL-C for MySQL is sharded physically for storage on N storage servers. Therefore, the I/O of a table is allocated to multiple disks, and the overall I/O throughput is much higher than that of centralized databases using local disks.

### Are there any limits on the numbers of databases and tables that I can create?
TDSQL-C for MySQL doesn't limit the numbers of databases and tables that can be created. Theoretically, you can create an unlimited number of databases and tables as long as there is enough space. For more information on how to view the upper limit of the storage space, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430).

### How do I create a database/table?
TDSQL-C for MySQL allows you to create a database/table in many ways:
- Quickly create a database/table in the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql) as instructed in [Creating Database](https://www.tencentcloud.com/document/product/1098/44606).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/MxbF364_14.png)
- Create a custom database/table through [DMC](https://dms.cloud.tencent.com/?resource-retry=2#/login?dbType=cynosdbmysql&region=ap-guangzhou&instanceId=cynosdbmysql-aaf8s18h).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ih2L156_15.png)
- Log in to the client as instructed in [Connecting to Cluster](https://www.tencentcloud.com/document/product/1098/51979) and run SQL commands to create a database/table.
The SQL statement to create a database is `create database`, and the command is:
```
create database <database name>;
```
The SQL statement to create a table is `create table`, and the command is:
```
create table <table name> (<table definition option>)<table option><partition option>;
The `<table definition option>` is in the format of `column name 1 type 1 [,...] column name n type n`.
```
Example: Create the `tb_emp1` table in the `test_db` database:
```
mysql> USE test_db;
Database changed
mysql> CREATE TABLE tb_emp1
    -> (
    -> id INT(11),
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT
    -> );
Query OK, 0 rows affected (0.37 sec)
```

### Which way is more appropriate to replicate a very big table in a TDSQL-C for MySQL database (for example, to replicate the entire table A to table B)?
You can use the following SQL statement for replication:
```
create table B as select * from A
```

### Does TDSQL-C for MySQL support table partitioning?
Yes. You can use partitioned tables to trim large tables to control the volume of data queried and accessed while remaining imperceptible to business code (with no modifications required).

### How do I quickly change the structure of a big table?
TDSQL-C for MySQL supports the instant DDL feature to quickly modify columns in big tables while avoiding data replication. This feature can implement changes in seconds without replicating data or using disk capacity or I/O during peak hours. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44589).
