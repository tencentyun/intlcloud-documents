This document describes more options on using COS-Hive connectors, where the data is from direct-insert, COS, and LZO.
## 1. Development Preparations
- This task requires access to COS, so you need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS first.
- Create an EMR cluster. When creating the EMR cluster, you need to select the Presto component on the software configuration page and enable access to COS on the basic configuration page.
- Relevant software programs such as Presto are installed in the `/usr/local/service/` directory of the CVM instance for the EMR cluster.

## 2. Data Preparations
First, log in to any node (preferably a master one) in the EMR cluster. For information about how to log in to EMR, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click **Login** on the right of the desired CVM instance to go to the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once your credentials are validated, you can enter the command line interface.

Run the following commands to switch to the Hadoop user and go to the Hive installation folder:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```
Create a file named `cos.txt` and add the following data to it:
```
5,cos_patrick
6,cos_stone
```
Upload the file to COS by running the following HDFS command. Here, `$bucketname` is the name plus path of the bucket you created.
```
[hadoop@172 hive]# hdfs dfs –put cosn://$bucketname/
```
Create a file named `lzo.txt` and add the following data to it:
```
10,lzo_pop
11,lzo_tim
```
Compress it into an .lzo file:
```
[hadoop@172 hive]$ lzop -v lzo.txt
compressing hive_test.data into lzo.txt.lzo
```

>!To create an .lzo compressed file, you need to install lzo and lzop first by running this command: `yum -y install lzo lzop`.

## 3. Creating a Hive Table and Using Presto for Query
A script file is used here to create a Hive database and table. Create a script file named presto_on_cos_test.sql and add the following program to it:
```
create database if not exists test;
use test;
create external table if not exists presto_on_cos (id int,name string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ’,’;
insert into presto_on_cos values (12,’hello’),(13,’world’);
load data inpath "cosn://$bucketname/cos.txt" into table presto_on_cos;
load data local inpath "/$yourpath/lzo.txt.lzo" into table presto_on_cos;
```
Here, $bucketname is the name plus path of your COS bucket, and $yourpath is the path where the lzo.txt.lzo file is stored.

The script file creates a database named "test" first and then a table named "presto_on_cos" in the created database. Here, the data is loaded in three steps: first, insert the data directly; then, insert the data stored in COS; and finally, insert the data stored in the .lzo package.

**It is recommended to use an external table for Hive testing as shown in this example so as to avoid deleting important data by mistake.** Run this script with Hive CLI:
```
[hadoop@172 hive]$ hive -f "presto_on_cos_test.sql"
```
Once the execution is completed, you can enter Presto to view the data in the table. Use the same method as described in the previous section to enter Presto, but you should modify the `schema` parameter.
```
[hadoop@172 presto-client]$ ./presto --server $host:$port --catalog hive --schema test
```
Query the Hive table you just created:
```
presto:test> select * from presto_on_cos ;
 id |    name     
----+-------------
  5 | cos_patrick 
  6 | cos_stone   
 10 | lzo_pop     
 11 | lzo_tim     
 12 | hello 
 13 | world 
(6 rows)

Query 20180702_150000_00011_c4qzg, FINISHED, 3 nodes
Splits: 4 total, 4 done (100.00%)
0:03 [6 rows, 127B] [1 rows/s, 37B/s]
```
For more information about Presto usage, see the [official documentation](https://prestodb.io/docs/current/).
