This document describes how to use Sqoop on EMR to import and export data between MySQL and Hive.
## 1. Preparations for Development
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, you need to select the Sqoop and Hive components on the software configuration page. 
- Relevant software programs such as Sqoop are installed in the `/usr/local/service/` directory of the CVM instance for the EMR cluster.

## 2. Importing Data from TencentDB for MySQL into Hive
This section continues with the use case from the previous section.
Enter the EMR Console and copy the instance ID of the target cluster, i.e., the cluster name. Then, enter the TencentDB for MySQL Console, use Ctrl+F to find the MySQL database corresponding to the cluster, and view its private IP address of the database (`$mysqlIP`).

Log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.
Run the following command on the EMR command line to switch to the Hadoop user and go to the Hive folder:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```
Create a Hive database:
```
[hadoop@172 hive]$ hive
hive> create database hive_from_sqoop;
OK
Time taken: 0.167 seconds
```
Import the MySQL database created in the previous section into Hive by running the `sqoop-import` command:
```
[hadoop@172 hive]# cd /usr/local/service/sqoop
[hadoop@172 sqoop]$ bin/sqoop-import --connect  jdbc:mysql://$mysqlIP/test --username 
root -P --table sqoop_test_back --hive-database hive_from_sqoop --hive-import --hive-table hive_from_sqoop
```
Here, `$mysqlIP` is the private IP address of your TencentDB for MySQL instance, `test` is the name of your MySQL database, `--table` is the name of the MySQL table to be exported, `--hive-database` is the name of your Hive database, and `--hive-table` is the name of the Hive table to be imported into.
Running this command requires the password of your MySQL database, which is the one you set when you created the EMR cluster.
After successful execution, you can view the imported database in Hive:
```
hive> select * from hive_from_sqoop;
OK
1	first	2018-07-03 16:07:46.0	spark
2	second	2018-07-03 15:30:57.0	mr
3	third	2018-07-03 15:31:07.0	yarn
4	forth	2018-07-03 15:39:38.0	hbase
5	fifth	2018-07-03 16:02:29.0	hive
6	sixth	2018-07-03 16:09:58.0	sqoop
Time taken: 1.245 seconds, Fetched: 6 row(s)
```

## 3. Importing Data from Hive into TencentDB for MySQL
Sqoop supports importing data from Hive tables into TencentDB for MySQL. To do so, create a table in Hive first and then import data.
Log in to any node (preferably a master one) in the EMR cluster. Run the following command on the EMR command line to switch to the Hadoop user and go to the Hive folder:

```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```
Create a Bash script file named `gen_data.sh` and add the following code to it:

```
#!/bin/bash
MAXROW=1000000 # Specify the number of data rows to be generated
for((i = 0; i < $MAXROW; i++))
do
　　　echo $RANDOM, \"$RANDOM\"
done
```
Run it as follows:
```
[hadoop@172 hive]$ ./gen_data.sh > hive_test.data
```

This script file will generate 1,000,000 random number pairs and save them to the `hive_test.data` file.
Run the following command to upload the generated test data to HDFS first:

```
[hadoop@172 hive]$ hdfs dfs -put ./hive_test.data /$hdfspath
```
Here, `$hdfspath` is the path to your file on HDFS.
Connect to Hive and create a test table:

```
[hadoop@172 hive]$ bin/hive
hive> create database hive_to_sqoop;          # Create the database `hive_to_sqoop`
OK
Time taken: 0.176 seconds
hive> use hive_to_sqoop;                            # Switch databases
OK
Time taken: 0.176 seconds
hive> create table hive_test (a int, b string)
hive> ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
　　　　　　　　　　　　　　　　# Create a data table named `hive_test` and specify the column separator as `,`
OK
Time taken: 0.204 seconds
hive> load data inpath "/$hdfspath/hive_test.data" into table hive_test;   # Import the data
```

`$hdfspath` is the path to your file stored in HDFS.
After success, you can run the `quit` command to exit the Hive data warehouse. Then, connect to TencentDB for MySQL and create a corresponding table:

```
[hadoop@172 hive]$ mysql -h $mysqlIP –p
Enter password:
```
Here, `$mysqlIP` is the private IP address of this database, and the password is the one you set when creating the cluster.
Create a table named `test` in MySQL. **Note that the field names in the MySQL table must be the same as those in the Hive table:**
```
mysql> create table table_from_hive (a int,b varchar(255));
```

You can exit MySQL after successfully creating the table.
There are two ways to import data from a Hive data warehouse into a TencentDB for MySQL database by using Sqoop: using the Hive data stored in HDFS directly or using HCatalog to import the data.

### Using Hive data stored in HDFS
Switch to the Sqoop folder and export the data from the Hive database to the TencentDB for MySQL database by running the following command:

```
[hadoop@172 hive]$ cd  ../sqoop/bin
[hadoop@172 bin]$ ./sqoop-export --connect jdbc:mysql://$mysqlIP/test --username root -P 
--table table_from_hive --export-dir /usr/hive/warehouse/hive_to_sqoop.db/hive_test
```
Here, `$mysqlIP` is the private IP address of your TencentDB for MySQL instance, `test` is the name of the MySQL database, `--table` is followed by the name of the table in the MySQL database, and `--export-dir` is followed by the location of the Hive table data stored in HDFS.

### Importing data by using HCatalog
Switch to the Sqoop folder and export the data from the Hive database to the TencentDB for MySQL database by running the following command:

```
[hadoop@172 hive]$ cd  ../sqoop/bin
[hadoop@172 bin]$ ./sqoop-export --connect jdbc:mysql://$mysqlIP/test --username root -P 
--table table_from_hive --hcatalog-database hive_to_sqoop --hcatalog-table hive_test
```
Here, `$mysqlIP` is the private IP address of your TencentDB for MySQL instance, `test` is the name of the MySQL database, `--table` is followed by the name of the table in the MySQL database, `-hcatalog-database` is followed by the name of the database where the Hive table to be exported is stored, and `--hcatalog-table` is followed by the name of the Hive table to be exported.
After the operation is completed, you can enter the MySQL database to see whether the import is successful:

```
[hadoop@172 hive]$ mysql -h $mysqlIP –p                  # Connect to MySQL
Enter password:
mysql> use test;
Database changed
mysql> select count(*) from table_from_hive;     # Now there are 1,000,000 data entries in the table
+----------+
| count(*) |
+----------+
| 1000000 |
+----------+
1 row in set (0.03 sec)
mysql> select * from table_from_hive limit 10;    # View the first 10 entries in the table
+-------+----------+
| a     | b        |
+-------+----------+
| 28523 |  "3394"  |
| 31065 |  "24583" |
|   399 |  "23629" |
| 18779 |  "8377"  |
| 25376 |  "30798" |
| 20234 |  "22048" |
| 30744 |  "32753" |
| 21423 |  "6117"  |
| 26867 |  "16787" |
| 18526 |  "5856"  |
+-------+----------+
10 rows in set (0.00 sec)
```
You can view more parameters about the `sqoop-export` command by running the following command:
```
[hadoop@172 bin]$ ./sqoop-export --help
```

## 4. Importing a Hive Table in ORC Format into TencentDB for MySQL
ORC is a columnar storage format that can greatly improve the performance of Hive. This section describes how to create an ORC table, load data into it, and then use the Sqoop on EMR to export the data stored in ORC format in Hive to TencentDB for MySQL.
>After importing a Hive table in ORC format to TencentDB for MySQL, you cannot use the data stored in HDFS directly; instead, you have to use HCatalog.

This section continues with the use case from the previous section.
Log in to a master node of the EMR cluster and run the following command on the EMR command line to switch to the Hadoop user and go to the Hive folder:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```
Create a table in the database `hive_from_sqoop` created in the previous section:
```
[hadoop@172 hive]$ hive
hive> use hive_to_sqoop;
OK
Time taken: 0.013 seconds
hive> create table if not exists orc_test(a int,b string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' stored as orc;
```
You can view the storage format of the data in the table by running the following command:	

```
hive> show create table orc_test;
OK
CREATE TABLE `orc_test`(
  `a` int,
  `b` string)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.orc.OrcSerde'
WITH SERDEPROPERTIES (
  'field.delim'=',',
  'serialization.format'=',')
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'
LOCATION
  'hdfs://HDFS2789/usr/hive/warehouse/hive_to_sqoop.db/orc_test'
TBLPROPERTIES (
  'COLUMN_STATS_ACCURATE'='{\"BASIC_STATS\":\"true\"}',
  'numFiles'='0',
  'numRows'='0',
  'rawDataSize'='0',
  'totalSize'='0',
  'transient_lastDdlTime'='1533563293')
Time taken: 0.041 seconds, Fetched: 21 row(s)
```
It can be seen from the returned data that the data storage format in the table is ORC.
There are several ways to import data into a Hive table in ORC format, but only one of them is described here, i.e., importing data into an ORC table by creating a temporary Hive table in text storage format. The table `hive_test` created in the previous section is used here as the temporary table, and the following command is used to import the data: 
```
hive> insert into table orc_test select * from hive_test;
```
After successful import, you can view the data in the table by running the `select` command.
Next, use Sqoop to export the Hive table in ORC format to MySQL.
Connect to TencentDB for MySQL and create a corresponding table. The specific way to connect is as described above.

```
[hadoop@172 hive]$ mysql -h $mysqlIP –p
Enter password:
```
Here, `$mysqlIP` is the private IP address of this database, and the password is the one you set when creating the cluster.
Create a table named `test` in MySQL. **Note that the field names in the MySQL table must be the same as those in the Hive table:**
```
mysql> create table table_from_orc (a int,b varchar(255));
```
You can exit MySQL after successfully creating the table.
Switch to the Sqoop folder and export the data in ORC format from the Hive database to the TencentDB for MySQL database by running the following command:

```
[hadoop@172 hive]$ cd  ../sqoop/bin
[hadoop@172 bin]$ ./sqoop-export --connect jdbc:mysql://$mysqlIP/test --username root -P 
--table table_from_orc --hcatalog-database hive_to_sqoop --hcatalog-table orc_test
```
Here, `$mysqlIP` is the private IP address of your TencentDB for MySQL instance, `test` is the name of the MySQL database, `--table` is followed by the name of the table in the MySQL database, `-hcatalog-database` is followed by the name of the database where the Hive table to be exported is stored, and `--hcatalog-table` is followed by the name of the Hive table to be exported.
After successful import, you can view the data in the corresponding table in the MySQL database:

```
mysql> select count(*) from table_from_orc;
+----------+
| count(*) |
+----------+
| 1000000 |
+----------+
1 row in set (0.24 sec)
mysql> select * from table_from_orc limit 10;
+-------+----------+
| a     | b        |
+-------+----------+
| 28523 |  "3394"  |
| 31065 |  "24583" |
|   399 |  "23629" |
| 18779 |  "8377"  |
| 25376 |  "30798" |
| 20234 |  "22048" |
| 30744 |  "32753" |
| 21423 |  "6117"  |
| 26867 |  "16787" |
| 18526 |  "5856"  |
+-------+----------+
10 rows in set (0.00 sec)
```

For more information on Sqoop usage, please see the [official documentation](http://sqoop.apache.org/docs/1.4.6/SqoopUserGuide.html).
