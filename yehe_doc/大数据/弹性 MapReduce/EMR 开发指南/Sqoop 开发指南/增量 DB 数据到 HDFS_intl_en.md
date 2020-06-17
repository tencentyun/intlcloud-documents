Sqoop is an open-source tool for transferring data between Hadoop and traditional databases such as MySQL and PostgreSQL. It can import data in a relational database (e.g., MySQL, Oracle, and Postgres) into Hadoop's HDFS, and vice versa. One of the highlights of Sqoop is its ability to import data in a relational database into HDFS through Hadoop MapReduce.

This document describes the incremental import operation of Sqoop, i.e., importing only new or updated data in the database into HDFS. This can be done in either append or lastmodified mode. The former can be used in the case where there is only new but not modified data in the database, while the latter can be used in either case.

## 1. Preparations for Development
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Sqoop component on the software configuration page. 
- Relevant software programs such as Sqoop are installed in the `/usr/local/service/` directory of the CVM instance for the EMR cluster.

## 2. Using the append Mode 
This section will continue to use the use case from the previous section.
Enter the EMR Console and copy the instance ID of the target cluster, i.e., the cluster name. Then, enter the TencentDB for MySQL Console, use Ctrl+F to find the MySQL database corresponding to the cluster, and view the private IP address of the database ($mysqlIP).

Log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user and go to the Sqoop folder:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/sqoop
```
Connect to the MySQL database:
```
[hadoop@172 sqoop]$ mysql -h $mysqlIP –p
Enter password:
```
The password is the one you set when you created the EMR cluster.
After connecting to the MySQL database, add a new data entry to the table sqoop_test, as shown below:
```
mysql> use test;
Database changed

mysql> insert into sqoop_test values(null, 'forth', now(), 'hbase');
Query ok, 1 row affected(0.00 sec)
```
View the data in the table:
```
Mysql> select * from sqoop_test;
+----+--------+---------------------+---------+
| id | title  | time                | content |
+----+--------+---------------------+---------+
|  1 | first  | 2018-07-03 15:29:37 | hdfs    |
|  2 | second | 2018-07-03 15:30:57 | mr      |
|  3 | third  | 2018-07-03 15:31:07 | yarn    |
|  4 | forth  | 2018-07-03 15:39:38  | hbase    |
+----+--------+---------------------+---------+
4 rows in set (0.00 sec)
```
Sync the new data entry in append mode to the HDFS path where the data in the previous section is stored:
```
[hadoop@172 sqoop]$ bin/sqoop-import --connect jdbc:mysql://$mysqlIP/test --username 
root -P --table sqoop_test --check-column id  --incremental append --last-value 3 --target-dir 
/sqoop
```
Here, $mysqlIP is the private IP address of your MySQL database.

To run the command, you need to enter the password for the database, which is defaulted to the password you set when you created the EMR cluster. There are more parameters than the normal sqoop-import command, where --check-column is the reference data during import, --incremental is the import mode (i.e., append in this example), and --last-value is the value of the reference data. All data entries that are newer than this value are imported into HDFS.
After successful execution, you can view the updated data in the corresponding directory of HDFS:
```
[hadoop@172 sqoop]$ hadoop fs -cat /sqoop/*
1, first, 2018-07-03 15:29:37.0,hdfs
2, second, 2018-07-03 15:30:57.0,mr
3, third, 2018-07-03 15:31:07.0,yarn
4,forth,2018-07-03 15:39:38.0,hbase
```

### Using a Sqoop job
To sync data to HDFS in append mode, you need to manually enter --last-value each time, but you can also use the Sqoop job method, where Sqoop automatically saves the value of last-value in the last successful import. To use it, you need to start the sqoop-metastore process in the following steps:

Start the sqoop-metastore process in conf/sqoop-site.xml first:
```
<property>
  <name>sqoop.metastore.client.enable.autoconnect</name>
  <value>ture</value>
</property>
```
Then, start the sqoop-metastore service in the bin directory:
```
./sqoop-metastore &
```

Create a Sqoop job by running the following command:
>This command is applicable to Sqoop 1.4.6.

```
[hadoop@172 sqoop]$ bin/sqoop job --create job1 -- import --connect
jdbc:mysql://$mysqlIP/test --username root -P --table sqoop_test --check-column id 
--incremental append --last-value 4 --target-dir /sqoop
```
Here, $mysqlIP is the private IP address of your MySQL database. With this command, a Sqoop job is successfully created, and each execution will automatically use the last modified value of last-value.

Add a new data entry to the table sqoop_test in the MySQL database:
```
mysql> insert into sqoop_test values(null, 'fifth', now(), 'hive');
Query ok, 1 row affected(0.00 sec)

Mysql> select * from sqoop_test;
+----+--------+---------------------+---------+
| id | title  | time                | content |
+----+--------+---------------------+---------+
|  1 | first  | 2018-07-03 15:29:37 | hdfs    |
|  2 | second | 2018-07-03 15:30:57 | mr      |
|  3 | third  | 2018-07-03 15:31:07 | yarn    |
|  4 | forth  | 2018-07-03 15:39:38  | hbase    |
|  5 | fifth  | 2018-07-03 16:02:29   | hive    |
+----+--------+---------------------+---------+
5 rows in set (0.00 sec)
```
Then, execute the Sqoop job:
```
[hadoop@172 sqoop]$ bin/sqoop job --exec job1
```

To run this command, you need to enter the password for your MySQL database. After successful execution, you can view the updated data in the corresponding directory of HDFS:
```
[hadoop@172 sqoop]$ hadoop fs -cat /sqoop/*
1, first, 2018-07-03 15:29:37.0,hdfs
2, second, 2018-07-03 15:30:57.0,mr
3, third, 2018-07-03 15:31:07.0,yarn
4,forth,2018-07-03 15:39:38.0,hbase
5,fifth,2018-07-03 16:02:29.0,hive
```

## 3. Using the lastmodified Mode
Create a Sqoop job in lastmodified mode of sqoop-import directly to first query the last modified time in sqoop_test:
```
mysql> select max(time) from sqoop_test;
```
Create a Sqoop job:
```
[hadoop@172 sqoop]$ bin/sqoop job --create job2 -- import --connect jdbc:mysql://$mysqlIP/test --username root -P --table sqoop_test --check-column time --incremental lastmodified --merge-key id --last-value '2018-07-03 16:02:29' --target-dir /sqoop
```
Here, $mysqlIP is the private IP address of your MySQL database. Several parameters are added, where --check-column must use a timestamp, --incremental selects the lastmodified mode, --merge-key selects the ID, and --last-value is the last modified time in the table that is queried. All modifications made after this time are synced to HDFS, and the Sqoop job automatically saves and updates the value each time.

Add data to the table sqoop_test in the MySQL database and make changes:
```
mysql> insert into sqoop_test values(null, 'sixth', now(), 'sqoop');
Query ok, 1 row affected(0.00 sec)

mysql> update sqoop_test set time=now(), content='spark' where id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1 changed: 1 warnings: 0

Mysql> select * from sqoop_test;
+----+--------+---------------------+---------+
| id | title  | time                | content |
+----+--------+---------------------+---------+
|  1 | first  | 2018-07-03 16:07:46 | spark    |
|  2 | second | 2018-07-03 15:30:57 | mr      |
|  3 | third  | 2018-07-03 15:31:07 | yarn    |
|  4 | forth  | 2018-07-03 15:39:38  | hbase    |
|  5 | fifth  | 2018-07-03 16:02:29   | hive    |
|  6 | fifth  | 2018-07-03 16:09:58   | sqoop    |
+----+--------+---------------------+---------+
6 rows in set (0.00 sec)
```
Execute the Sqoop job:
```
[hadoop@172 sqoop]$ bin/sqoop job --exec job2
```

To run this command, you need to enter the password for your MySQL database. After successful execution, you can view the updated data in the corresponding directory of HDFS:
```
[hadoop@172 sqoop]$ hdfs dfs -cat /sqoop/*
1,first,2018-07-03 16:07:46.0,spark
2,second,2018-07-03 15:30:57.0,mr
3,third,2018-07-03 15:31:07.0,yarn
4,forth,2018-07-03 15:39:38.0,hbase
5,fifth,2018-07-03 16:02:29.0,hive
6,sixth,2018-07-03 16:09:58.0,sqoop
```
For more information on Sqoop usage, please see the [official documentation](http://sqoop.apache.org/docs/1.4.6/SqoopUserGuide.html).
