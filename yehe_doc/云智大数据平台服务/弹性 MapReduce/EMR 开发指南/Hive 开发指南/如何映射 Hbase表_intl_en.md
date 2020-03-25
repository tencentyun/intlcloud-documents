You can use Hive to map HBase tables. By doing so, you can read data in HBase with Hive and run Hive-SQL statements to perform operations such as query and insertion on HBase tables.
## 1.	Preparations for Development
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Hive and HBase components on the software configuration page. 
- Hive and its dependencies are installed under the EMR cluster directory `/usr/local/service/`

## 2.	Creating an HBase Table 
First, you need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user and go to the HBase folder to enter HBase Shell:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]# cd /usr/local/service/hbase
[hadoop@10hbase]$ bin/hbase shell
```
Create a table in HBase as shown below:
```
hbase(main):001:0> create 'test', 'cf'
hbase(main):003:0> put 'test', 'row1', 'cf:a', 'value1'
hbase(main):004:0> put 'test', 'row1', 'cf:b', 'value2'
hbase(main):005:0> put 'test', 'row1', 'cf:c', 'value3'
```
For more information on HBase operations, please see the Hbase Operation Guide or [official documentation](http://hbase.apache.org/book.html#_introduction).
After the creation is completed, you can use the `list` and `scan` operations to view the newly created table.
```
hbase(main):001:0> list 'test'
TABLE                                                       
test                                                         
1 row(s) in 0.0030 seconds
=> ["test"]

hbase(main):002:0> scan 'test'
ROW  COLUMN+CELL                                             
row1   column=cf:a, timestamp=1530276759697, value=value1   
row2   column=cf:b, timestamp=1530276777806, value=value2   
row3   column=cf:c, timestamp=1530276792839, value=value3   
3 row(s) in 0.2110 seconds
```
## 3.	Mapping a Hive Table
Switch to the Hive folder and connect to Hive:
```
[hadoop@172 hive]$ cd /usr/local/service/hive/
[hadoop@172 hive]$ bin/hive
```
Next, create a Hive external table and map it to the HBase table created in step 2:
```
hive> CREATE EXTERNAL TABLE hive_test (
    > rowkey string,
    > a string,
    > b string,
    > c string
    > ) STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' WITH
    > SERDEPROPERTIES("hbase.columns.mapping" = ":key,cf:a,cf:b,cf:c")
    > TBLPROPERTIES("hbase.table.name" = "test");
OK
Time taken: 2.086 seconds
```
Now, a mapping from the Hive table to the HBase is created. You can run the following command to view the elements in the Hive table:
```
hive> select * from hive_test;
OK
row1 value1	value2 value3
Time taken: 0.305 seconds, Fetched: 1 row(s)
```

