Hive is a data warehouse architecture built on the Hadoop file system (HDFS). It provides many functions for data warehouse management, such as data ETL (extraction, transformation, and loading), data storage management, and query and analysis for large data sets. In addition, it also defines the SQL-like language Hive-SQL, which allows users to perform operations similar to those in SQL. Hive-SQL maps structured data files to a single database table and provides simple SQL query capabilities. It also enables developers to easily use Mapper and Reducer operations to convert SQL statements into MapReduce jobs. This is a powerful support for the MapReduce framework, as the learning cost is low, and MapReduce statistics can be quickly collected with ease through SQL-like statements, eliminating the need to develop dedicated MapReduce applications. All these advantages make Hive very suitable for statistical analysis of data warehouses.

Hive uses Hadoop's HDFS as its file storage system, making it easy to expand the storage capacity and increase the computing power. It can achieve the same horizontal stability as that of Hadoop, so that a cluster of thousands of servers can be built conveniently. In general, Hive is designed for mining massive amounts of data, but its real-time performance is relatively poor.

This document mainly describes Hive's internal and external tables.
- An internal table actually maps a file in HDFS to a table, and the data warehouse of Hive generates the corresponding directory for it. The default warehouse path in EMR is `usr/hive/warehouse/$tablename`. **This path is in HDFS**, where `$tablename` is the name of the table you created. Simply load the files matching the table definition into this directory, and they can be queried with Hive-SQL.
An external table in Hive is very similar to a common table, except that the data is stored somewhere else but not in the directories of the table. The advantage of this mechanism is that when you delete the external table, the data it points to will not be deleted; instead, only the metadata corresponding to it will be deleted. On contrast, if you delete an internal table, all the data in it, including the metadata, will be deleted.

This document demonstrates how to create tables in an EMR cluster and query them through Hive.

## 1. Preparations for Development
- You need to create a bucket in COS for this job. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Hive component on the software configuration page and "Enable COS" on the basic configuration page and enter your own SecretId and SecretKey below, which can be viewed in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. If there is no key yet, click **Create Key** to create one.
- Hive and its dependencies are installed in the EMR cluster directory `/usr/local/service/`.

### 2. Data Preparations
First, you need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user, then go to the Hive installation folder:

```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```

Create a bash script file named gen_data.sh and add the following code to it:

```
#!/bin/bash
MAXROW=1000000 # Specify the number of data rows to be generated
for((i = 0; i < $MAXROW; i++))
do
    echo $RANDOM, \"$RANDOM\"
done
```
And run it as follows:

```
[hadoop@172 hive]$ chmod +x script name
[hadoop@172 hive]$ ./gen_data.sh > hive_test.data
```

This script file will generate 1,000,000 random number pairs and save them to the hive_test.data file.
Run the following command to upload the generated test data to HDFS first:
```
[hadoop@172 hive]$ hdfs dfs -put ./hive_test.data /$hdfspath
```
Here, $hdfspath is the path of your file on HDFS.
You can also use the data stored in COS. First, upload the data to COS. If the data is in the local file system, use the COS Console. If it is in your EMR cluster, run the following command:
```
[hadoop@172 hive]$ hdfs dfs -put ./hive_test.data cosn://$bucketname/
```
$bucketname is the name of the COS bucket you created.

## 3. Basic Operations of Hive
### Connecting to Hive
Log in to a master node of the EMR cluster, switch to the Hadoop user, go to the Hive directory, and connect to Hive by running the following command:

```
[hadoop@172 hive]$ su hadoop
[hadoop@172 hive]$ cd /usr/local/service/hive/bin
[hadoop@172 bin]$ hive
```
You can use the `-h` parameter to get basic information on Hive commands.
You can also use the Beeline mode to connect to a database. To do so, you also need to log in to a master node in EMR, switch to the Hadoop user, and go to the Hive directory. In the `conf/hive-site.xml` configuration file, get the connection port $port and host address $host of Hive server 2:

```
<property>
        <name>hive.server2.thrift.bind.host</name>
        <value>$host</value>
</property>
<property>
        <name>hive.server2.thrift.port</name>
        <value>$port</value>
</property>
```
In the bin directory, run the following statement to connect to Hive:

```
[hadoop@172 hive]$ cd bin
[hadoop@172 bin]$ ./beeline -u "jdbc:hive2:// $host: $port " -n hadoop -p hadoop
```

### Creating a Hive table
You run the same Hive-SQL statements in Hive mode and the Beeline mode. The following example shows how to run Hive-SQL statements in Hive mode.

Run the following command in Hive to view the database:

```
hive> show databases;
OK
default
Time taken: 0.26 seconds, Fetched: 1 row(s)
```
Run the `create` command to create a database:

```
hive> create database test;                  # Create a database named test
OK
Time taken: 0.176 seconds
```
Run the `use` command to go to the test database you just created:

```
hive> use test; 
OK
Time taken: 0.176 seconds
```
Run the `create` command to create an internal table named hive_test in the test database:

```
hive> create table hive_test (a int, b string)
hive> ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
# Create a data table named hive_test and specify the column separator as ','
OK
Time taken: 0.204 seconds
```
**There is only one command. If you do not enter the semicolon ";", Hive-SQL can put one command in multiple lines for input.**
Finally, you can run the following command to see whether the table has been created successfully:

```
hive> show tables;
OK
hive_test 
Time taken: 0.176 seconds, Fetched: 1 row(s)
```

### Importing data into a table
For data stored in HDFS, run the following command to import it into the table:
```
hive> load data inpath "/$hdfspath/hive_test.data" into table hive_test;
```
Here, $hdfspath is the path of your file in HDFS. After the import is completed, the source data file in the import path in HDFS will be deleted.
For data stored in COS, run the following command to import it into the table:
```
hive> load data inpath "cosn://$bucketname/hive_test.data" into table hive_test;
```
Here, $bucketname is your bucket name plus the path of the data in the bucket. Also, after the import is completed, the source data file in the import path in COS will be deleted.
You can also import data stored locally in the EMR cluster into Hive by running the following command:
```
hive>load data local inpath "/$localpath/hive_test.data" into table hive_test;
```
Here, $localpath is the path of the data locally stored in the EMR cluster. After the import is completed, the source data will be deleted.

### Running a query
Run the `select` command to perform a query and count the number of data rows in a table:

```
hive> select count(*) from hive_test;
Query ID = hadoop_20170316142922_967b5f0e-1f89-4464-bfa3-b6ed53273fc2
Total jobs = 1
Launching Job 1 out of 1
Number of reduce tasks determined at compile time: 1
In order to change the average load for a reducer (in bytes):
set hive.exec.reducers.bytes.per.reducer=
In order to limit the maximum number of reducers:
set hive.exec.reducers.max=
In order to set a constant number of reducers:
set mapreduce.job.reduces=
Starting Job = job_1489458311206_9869, Tracking URL =
http://10.0.1.125:5004/proxy/application_1489458311206_9869/
Kill Command = /usr/local/service/hadoop/bin/hadoop job -kill job_1489458311206_9869
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
2017-03-16 14:29:29,023 Stage-1 map = 0%, reduce = 0%
2017-03-16 14:29:34,208 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 3.87 sec
2017-03-16 14:29:40,404 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 5.79 sec
MapReduce Total cumulative CPU time: 5 seconds 790 msec
Ended Job = job_1489458311206_9869
MapReduce Jobs Launched:
Stage-Stage-1: Map: 1 Reduce: 1 Cumulative CPU: 5.79 sec
HDFS Read: 40974623 HDFS Write: 107 SUCCESS
Total MapReduce CPU Time Spent: 5 seconds 790 msec
OK
1000000
Time taken: 18.504 seconds, Fetched: 1 row(s)
```
The final output is 1000000.
Run the `select` command to query the first 10 elements in the table:

```
hive> select * from hive_test limit 10;
OK
30847	"31583"
14887	"32053"
19741	"16590"
8104	"20321"
29030	"32724"
27274	"5231"
10028	"22594"
924	"32569"
10603	"27927"
4018	"30518"
Time taken: 2.133 seconds, Fetched: 10 row(s)
```

### Deleting a Hive table
Run the `drop` command to delete a Hive table:

```
hive> drop table hive_test;
Moved: 'hdfs://HDFS/usr/hive/warehouse/hive_test' to trash at: hdfs://HDFS/user/hadoop/.Trash/Current
OK
Time taken: 2.327 seconds
```
For more information on Hive operations, please see the [official documentation](https://hive.apache.org/).
　　　
