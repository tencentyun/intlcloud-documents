Sqoop is an open-source tool for transferring data between Hadoop and traditional databases such as MySQL and PostgreSQL. It can import data in a relational database (e.g., MySQL, Oracle, and Postgres) into Hadoop's HDFS, and vice versa. One of the highlights of Sqoop is its ability to import data in a relational database into HDFS through Hadoop MapReduce.

This document describes how to use Sqoop on EMR to import and export data between MySQL and HDFS.

## 1. Prerequisites
- You have signed up for a Tencent Cloud account and created an EMR cluster. When creating the EMR cluster, select the Sqoop component on the software configuration page.
- Relevant software programs such as Sqoop are installed in the `/usr/local/service/` directory of the CVM instance for the EMR cluster.

## 2. Creating a MySQL Table
Connect to the created MySQL database first. Enter the EMR Console and copy the instance ID of the destination cluster, i.e., the cluster name. Then, enter the TencentDB for MySQL Console, use Ctrl+F to find the MySQL database corresponding to the cluster, and view the private IP address of the database ($mysqlIP).

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

After connecting to the MySQL database, enter the test database and create a table. You can also choose the destination database:
```
mysql> use test;
Database changed

mysql> create table sqoop_test(id int not null primary key auto_increment, title varchar(64), time timestamp, content varchar(255));
Query ok , 0 rows affected(0.00 sec)
```
This command creates a MySQL table with a primary key of ID and three columns of title, time, and content. Insert data entries into the table as follows:
```
mysql> insert into sqoop_test values(null, 'first', now(), 'hdfs');
Query ok, 1 row affected(0.00 sec)

mysql> insert into sqoop_test values(null, 'second', now(), 'mr');
Query ok, 1 row affected (0.00 sec)

mysql> insert into sqoop_test values(null, 'third', now(), 'yarn');
Query ok, 1 row affected(0.00 sec)
```
Run the following command to view the data in the table:
```
Mysql> select * from sqoop_test;
+----+--------+---------------------+---------+
| id | title  | time                | content |
+----+--------+---------------------+---------+
|  1 | first  | 2018-07-03 15:29:37 | hdfs    |
|  2 | second | 2018-07-03 15:30:57 | mr      |
|  3 | third  | 2018-07-03 15:31:07 | yarn    |
+----+--------+---------------------+---------+
3 rows in set (0.00 sec)
```
Exit the MySQL database:
```
Mysql> exit;
```

## 3. Importing MySQL Data into HDFS
Run the sqoop-import command to import the data from the sqoop_test table created in the previous step into HDFS:
```
[hadoop@172 sqoop]$ bin/sqoop-import --connect jdbc:mysql://$mysqlIP/test --username root 
-P --table sqoop_test --target-dir /sqoop
```
Here, --connect is used to connect to the MySQL database, test can be replaced with your database name, -P indicates that a password is required, --table is the name of the database you want to export, --target-dir is the path in HDFS to import into. **Make sure that the `/sqoop` folder does not exist before the command is run; otherwise, a failure will occur.**

After you press Enter, you will be asked for a password, which is the one set when you created the EMR cluster.

After successful execution, you can view the imported data in the corresponding path in HDFS:
```
[hadoop@172 sqoop]$ hadoop fs -cat /sqoop/*
1, first, 2018-07-03 15:29:37.0,hdfs
2, second, 2018-07-03 15:30:57.0,mr
3, third, 2018-07-03 15:31:07.0,yarn
```

## 4. Importing HDFS Data into MySQL
You need to create a table in MySQL first to store the data from HDFS:
```
[hadoop@172 sqoop]$ mysql -h $mysqlIP –p
Enter password:
mysql> use test;
Database changed

mysql> create table sqoop_test_back(id int not null primary key auto_increment, title varchar(64), time timestamp, content varchar(255));
Query ok , 0 rows affected(0.00 sec)
```
Check whether the table is created successfully and then exit MySQL:
```
mysql> show tables;                                                                     
+-----------------+
| Tables_in_test  |
+-----------------+
| sqoop_test      |
| sqoop_test_back |
+-----------------+
2 rows in set (0.00 sec)

mysql> exit;
```
Run the sqoop-export command to export the data imported into HDFS in the previous step into MySQL:
```
[hadoop@172 sqoop]$ bin/sqoop-export --connect jdbc:mysql://172.16.16.42/test --username 
root -P --table sqoop_test_back --export-dir /sqoop
```
The parameters are similar to those for sqoop-import, except --export-dir, which is the path of the data in HDFS. You also need to enter the password after pressing Enter.

After successful execution, you can verify the data in the database sqoop_test_back:
```
[hadoop@172 sqoop]$ mysql -h $mysqlIP –p
Enter password:
mysql> use test;
Database changed

mysql> select * from sqoop_test_back;
+----+---------+---------------------+---------+
| id | title   | time                | content |
+----+---------+---------------------+---------+
|  1 | first   | 2018-07-03 15:29:37 | hdfs   |
|  2 | second  | 2018-07-03 15:30:57 | mr      |
|  3 | third   | 2018-07-03 15:31:07 | yarn    |
+----+---------+---------------------+---------+
3 rows in set (0.00 sec)
```
For more information about Sqoop usage, please see the [official documentation](http://sqoop.apache.org/docs/1.4.6/SqoopUserGuide.html).
　　　
