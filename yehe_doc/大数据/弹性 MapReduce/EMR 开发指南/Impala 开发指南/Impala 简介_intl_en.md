Apache Impala provides high-performance and low-latency SQL queries on data stored in Apache Hadoop file formats. Its fast response to queries enables interactive exploration and fine-tuning of analytical queries rather than long batch jobs traditionally associated with SQL-on-Hadoop technologies.

Impala differs from Hive in that Hive uses the MapReduce engine for execution and involves batch processing, while Impala streams intermediate results over the internet instead of writing them to the disk, which greatly reduces the I/O overheads of nodes.

Impala integrates with Apache Hive database to share databases and tables between both components. The high level of integration with Hive and compatibility with the HiveQL syntax enable you to use either Impala or Hive to create tables, initiate queries, load data, and do more.

## Prerequisites
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Impala component on the software configuration page.
- Impala is installed in the `/data/Impala` directory of the CVM instance for the EMR cluster.

## Data Preparations
Log in to any node (preferably a master one) in the EMR cluster first. For more information on how to log in to EMR, see [Logging In To Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436). You can choose to log in with WebShell. Click **Login** on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following commands to switch to the Hadoop user and go to the Impala folder:
```swift
[root@10 ~]# su hadoop
[hadoop@10 root]$ cd /data/Impala/
```
Create a bash script file named `gen_data.sh` and add the following code to it:
```swift
#!/bin/bash
MAXROW=1000000 # Specify the number of data rows to be generated
for((i = 0; i < $MAXROW; i++))
do
      echo $RANDOM, \"$RANDOM\"
done
```
Then, run the following command:
```swift
[hadoop@10 ~]$ ./gen_data.sh > impala_test.data
```
This script file will generate 1,000,000 random number pairs and save them to the `impala_test.data` file. Then, upload the generated test data to HDFS and run the following commands:
```swift
[hadoop@10 ~]$ hdfspath="/impala_test_dir"
[hadoop@10 ~]$ hdfs dfs -mkdir $hdfspath
[hadoop@10 ~]$ hdfs dfs -put ./impala_test.data $hdfspath
```
Here, `$hdfspath` is the path of your file in HDFS. Finally, you can run the following command to verify whether the data has been properly put in HDFS.
```swift
[hadoop@10 ~]$ hdfs dfs -ls $hdfspath
```


## Basic Impala Operations
The `impala-shell` path varies by the community component API protocol and default path of the Impala version as shown below:

| lmpala Version | impala-shell Path | Default Communication Port of impala-shell |
|---------|---------|---------|
| 4.1.0/4.0.0 | /data/lmpala/shell | 27009 |
| 3.4.0|  /data/lmpala/shell | 27001| 
| 2.10.0  | /data/lmpala/bin | 27001| 

The following takes Impala 3.4.0 as an example:
### Connecting to Impala
Log in to a master node in the EMR cluster, switch to the Hadoop user, go to the Impala directory, and connect to Impala:
```swift
[root@10 Impala]# cd /data/Impala/shell;./impala-shell -i $core_ip:27001
```
Here, `core_ip` is the IP of the core node of the EMR cluster. The IP of a task node can also be used. After login succeeds, the following will be displayed:
```swift
Connected to $core_ip:27001
Server version: impalad version 3.4.1-RELEASE RELEASE (build Could not obtain git hash)
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell 3.4.1-RELEASE (ebled66) built on Tue Nov 20 17:28:10 CST 2021)

The SET command shows the current value of all shell and query options.
***********************************************************************************
[$core_ip:27001] >
```
You can also directly connect to Impala by executing the following statement after logging in to the core node or task node:
```swift
cd /data/Impala/shell;./impala-shell -i localhost:27001
```
 
### Creating an Impala database
Run the following statement in Impala to view the database:
```swift
[10.1.0.215:27001] > show databases;
Query: show databases
+------------------+----------------------------------------------+
| name             | comment                                      |
+------------------+----------------------------------------------+
| _impala_builtins | System database for Impala builtin functions |
| default          | Default Hive database                        |
+------------------+----------------------------------------------+
Fetched 2 row(s) in 0.09s
```
Run the `create` command to create a database:
```swift
[localhost:27001] > create database experiments;
Query: create database experiments
Fetched 0 row(s) in 0.41s
```
Run the `use` command to go to the `test` database you just created:
```swift
[localhost:27001] > use experiments;
Query: use experiments
```
View the current database and execute the following statement:
```swift
select current_database();
```

### Creating an Impala table
Run the `create` command to create an internal table named `impala_test` in the `experiments` database:
```swift
[localhost:27001] > create table t1 (a int, b string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
Query: create table t1 (a int, b string)
Fetched 0 row(s) in 0.13s
```
View all tables:
```swift
[localhost:27001] > show tables;
Query: show tables
+------+
| name |
+------+
| t1   |
+------+
Fetched 1 row(s) in 0.01s
```
View the table structure:
```swift
[localhost:27001] > desc t1;
Query: describe t1
+------+--------+---------+
| name | type   | comment |
+------+--------+---------+
| a    | int    |         |
| b    | string |         |
+------+--------+---------+
Fetched 2 row(s) in 0.01s
```

### Importing data into a table
For data stored in HDFS, run the following command to import it into the table:
```swift
LOAD DATA INPATH '$hdfspath/impala_test.data' INTO TABLE t1;
```
Here, `$hdfspath` is the path of your file in HDFS. After the import is completed, the source data file in the import path in HDFS will be deleted and then stored in the `/usr/hive/warehouse/experiments.db/t1` path of the Impala internal table. You can also create an external table by running the following statement:
>!There is only one command. If you do not enter the semicolon ";", you can put one command in multiple lines for input.
>
```swift
CREATE EXTERNAL TABLE t2
(
   a INT,
   b string
)  
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
LOCATION '/impala_test_dir';
```

### Running a query
```swift
[localhost:27001] > select count(*) from experiments.t1;
Query: select count(*) from experiments.t1
Query submitted at: 2019-03-01 11:20:20 (Coordinator: http://10.1.0.215:20004)
Query progress can be monitored at: http://10.1.0.215:20004/query_plan?query_id=f1441478dba3a1c5:fa7a8eef00000000
+----------+
| count(*) |
+----------+
| 1000000  |
+----------+
Fetched 1 row(s) in 0.63s
```
The final output is 1000000.

### Deleting a table
```swift
[localhost:27001] > drop table experiments.t1;
Query: drop table experiments.t1
```

For more information on Impala operations, see the [official documentation](https://impala.apache.org/impala-docs.html).

## Connecting to Impala Through JDBC
Impala can also be connected through Java code by following the steps similar to those described in [Connecting to Hive Through Java](https://intl.cloud.tencent.com/document/product/1026/31147).

The only difference is `$hs2host` and `$hsport`, where `$hs2host` is the IP of any core node or task node in the EMR cluster and `$hsport` can be viewed in the `conf/impalad.flgs` configuration file under the Impala directory of the corresponding node.
```swift
[root@10 ~]# su hadoop
[hadoop@10 root]$ cd /data/Impala/
[hadoop@10 Impala]$ grep hs2_port conf/impalad.flgs
```

## Mapping an HBase Table
Impala uses Hive metadata, and all tables in Hive can be read in Impala. For more information on how to map an HBase table in Impala, see [Mapping HBase Tables](https://intl.cloud.tencent.com/document/product/1026/31149).

