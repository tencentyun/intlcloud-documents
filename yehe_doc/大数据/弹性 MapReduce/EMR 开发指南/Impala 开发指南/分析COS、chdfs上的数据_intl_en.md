This document describes more ways to use Impala based on COS with data from direct data insertion and COS.

## Development Preparations
1. This task requires access to COS, so you need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS first.
2. Create an EMR cluster. When creating the EMR cluster, you need to select the Impala component on the software configuration page and enable access to COS on the basic configuration page.
3. Relevant software programs such as Impala are installed in the `/usr/local/service/` directory of the CVM instance for the EMR cluster.

## Directions
Log in to any node (preferably a master one) in the EMR cluster first. For more information on how to log in to EMR, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can choose to log in with WebShell. Click **Login** on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct information is entered, you can enter the command line interface.

Run the following commands on the EMR command line to switch to the Hadoop user and connect to Impala:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]$ impala-shel.sh -i $host:27001
```
`$host` is the private IP of your Impala data node.

### Step 1. Create a table (record)
```
[$host:27001 ] > create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile location 'cosn://$bucketname/';
Query: create table record(id int, name string) row format delimited fields terminated by ',' stored as textfile location 'cosn://$bucketname/'
Fetched 0 row(s) in 3.07s
Here, `$bucketname` is the name plus path of your COS bucket. If you use CHDFS, replace the `location` value with `ofs://$mountname/`, where `$mountname` is your CHDFS instance mount address plus path.
View the table information and confirm that `location` is the COS path.
[$host:27001 ] > show create table record2;
Query: show create table record2
+----------------------------------------------------------------------+
| result                                                               |
+----------------------------------------------------------------------+
| CREATE TABLE default.record2 (                                       |
|   id INT,                                                            |
|   name STRING                                                        |
| )                                                                    |
| ROW FORMAT DELIMITED FIELDS TERMINATED BY ','                        |
| WITH SERDEPROPERTIES ('field.delim'=',', 'serialization.format'=',') |
| STORED AS TEXTFILE                                                   |
| LOCATION 'cosn://$bucketname'                                 |
| TBLPROPERTIES ('numFiles'='19', 'totalSize'='1870')                  |
+----------------------------------------------------------------------+
Fetched 1 row(s) in 5.90s
```

### Step 2. Insert data into the table
```
[$host:27001] > insert into record values(1,"test");
Query: insert into record values(1,"test")
Query submitted at: 2020-08-03 11:29:16 (Coordinator: http://$host:27004)
Query progress can be monitored at: http:/$host:27004/query_plan?query_id=b246d3194efb7a8f:bc60721600000000
Modified 1 row(s) in 0.64s
```

### Step 3. Use Impala to query the table
```
[$host:27001] > select * from record;
Query: select * from record
Query submitted at: 2020-08-03 11:29:31 (Coordinator: http://172.30.1.136:27004)
Query progress can be monitored at: http://$host:27004/query_plan?query_id=8148da96f8c0d369:4b26432a00000000
+----+---------+
| id | name    |
+----+---------+
| 1  | test    |
+----+---------+
Fetched 1 row(s) in 0.37s
```
