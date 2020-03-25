This section shows more options on using COS-Hive connectors, where the data is from direct-insert, COS, and LZO.
## 1.	Preparations for Development
- You need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS for this job.
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Presto component on the software configuration page and "Enable COS" on the basic configuration page and enter your own SecretId and SecretKey below.
They can be viewed in the [API Key Management](https://console.cloud.tencent.com/cam/capi) page. If there is no key yet, click **Create Key** to create one.
- Relevant software programs such as Presto are installed in the ` /usr/local/service/` directory of the CVM instance for the EMR cluster.

## 2.	Data Preparations
First, log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click *Login* button on the right of the desired CVM instance and then enter the login page. The default username is root, and the password is the one you set when you created the EMR cluster. Once your credentials have been validated, you can access the command-line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user, then go to the Hive installation folder:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hive
```
Create a file named cos.txt and add the following data to it:
```
5,cos_patrick
6,cos_stone
```
Upload the file to COS by running the following HDFS command. Here, $bucketname is the name plus path of the bucket you created.
```
[hadoop@172 hive]# hdfs dfs –put cosn://$bucketname/
```
Create a file named lzo.txt and add the following data to it:
```
10,lzo_pop
11,lzo_tim
```
Compress it into an .lzo file:
```
[hadoop@172 hive]$ lzop -v lzo.txt
compressing hive_test.data into lzo.txt.lzo
```

>To create an .lzo compressed file, you need to install lzo and lzop first by running the following command: `yum -y install lzo lzop`.

## 3.	Creating a Hive Table and Using Presto for Query
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

**You are recommended to use an external table for Hive testing as shown in this example so as to avoid deleting important data by mistake.** Run this script with Hive CLI:

```
[hadoop@172 hive]$ hive -f "presto_on_cos_test.sql"
```

Once the execution is completed, you can enter Presto to view the data in the table. Use the same method as described in the previous section to enter Presto, but you should modify the schema parameter.

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
For more information on Presto usage, please see the [official documentation](https://prestodb.io/docs/current/).
