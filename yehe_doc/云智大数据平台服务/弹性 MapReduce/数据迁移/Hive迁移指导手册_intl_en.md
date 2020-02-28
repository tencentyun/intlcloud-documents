Hive migration involves migration of data and metadata. Hive table data is mainly stored in HDFS; therefore, data migration is usually implemented at the HDFS layer. Hive metadata is mainly stored in a relational database and thus can be smoothly migrated to TencentDB for MySQL with guaranteed high availability.

### Migrating Hive Metadata

1. Dump the source Hive metastore.
```
mysqldump -hX.X.X.X -uroot -pXXXX --single-transaction --set-gtid-purged=OFF hivemetastore > hivemetastore-src.sql  
# If GTID is not enabled for MySQL, please delete `--set-gtid-purged=OFF` from the command  
# `X.X.X.X` is the IP address of the database server  
# `XXXX` is the database password  
# If the database user is not `root`, use the correct username  
# `hivemetastor` is the Hive metastore name 
```
2. Confirm the default path of the target Hive table data in HDFS.
The default path of the Hive table data in HDFS is specified by `hive.metastore.warehouse.dir` in `hive-site.xml`. If the storage location of the Hive table in HDFS is to be kept the same as that in the source Hive database, you need to modify this parameter to the same value as that in the source Hive database.

 For example, if the value of `hive.metastore.warehouse.dir` in the source `hive-site.xml` is as follows:
```
<property>  
    <name>hive.metastore.warehouse.dir</name>  
    <value>/apps/hive/warehouse</value>  
</property>  
```

 Then, the value of `hive.metastore.warehouse.dir` in the target `hive-site.xml` should be as follows:
```
<property>  
    <name>hive.metastore.warehouse.dir</name>  
    <value>/usr/hive/warehouse</value>  
</property>  
```
If the storage location of the Hive table in HDFS is to be kept the same as that in the source Hive database, modify `hive.metastore.warehouse.dir` in the target `hive-site.xml` to the following value:
```
<property>  
    <name>hive.metastore.warehouse.dir</name>  
    <value>/apps/hive/warehouse</value>  
</property>  
```
3. Confirm the `SDS.LOCATION` and `DBS.DB_LOCATION_URI` fields of the target Hive metadata.
Run the following query statements to get the current `SDS.LOCATION` and `DBS.DB_LOCATION_URI` fields.
```
SELECT DB_LOCATION_URI from DBS;  
SELECT LOCATION from SDS; 
```
The query result is similar to the following:
```
mysql> SELECT LOCATION from SDS;  
+--------------------------------------------------+  
| LOCATION |  
+--------------------------------------------------+  
| hdfs://HDFS2648/usr/hive/warehouse/hitest.db/t1 |  
| hdfs://HDFS2648/usr/hive/warehouse/wyp |  
+--------------------------------------------------+  
mysql> SELECT DB_LOCATION_URI from DBS;  
+-----------------------------------------------+  
| DB_LOCATION_URI |  
+-----------------------------------------------+  
| hdfs://HDFS2648/usr/hive/warehouse |  
| hdfs://HDFS2648/usr/hive/warehouse/hitest.db |  
+-----------------------------------------------+ 
```

 Here, `hdfs://HDFS2648` is the default file system name of HDFS, which is specified by `fs.defaultFS` in `core-site.xml`.
```
<property>  
    <name>fs.defaultFS</name>  
    <value>hdfs://HDFS2648</value>  
</property> 
```
`/usr/hive/warehouse` is the default storage path of the Hive table in HDFS, which is specified by `hive.metastore.warehouse.dir` in `hive-site.xml`.

 Therefore, you need to modify the `SDS.LOCATION` and `DBS.DB_LOCATION_URI` fields in the SQL file of the Hive metadata and make sure that the two fields in the imported Hive metastore use the correct path.

 You can run the following `sed` command to modify SQL files in batches.
```
Replace the IP: sed -i 's/oldcluster-ip:4007/newcluster-ip:4007/g' hivemetastore-src.sql  
Replace the default file system: sed -i 's/old-defaultFS/new-defaultFS/g' hivemetastore-src.sql  
```
4. Stop the MetaStore, HiveServer2, and WebHcataLog services of the target Hive database.
5. Back up the target Hive metastore.
```
mysqldump -hX.X.X.X -uroot -pXXXX --single-transaction --set-gtid-purged=OFF hivemetastore > hivemetastore-target.sql  
# If GTID is not enabled for MySQL, please delete `--set-gtid-purged=OFF` from the command  
# `X.X.X.X` is the IP address of the database server  
# `XXXX` is the database password  
# If the database user is not `root`, use the correct username  
# `hivemetastor` is the Hive metastore name 
```
6. Drop and create the target Hive metastore.
```
mysql> drop database hivemetastore;  
mysql> create database hivemetastore; 
```
7. Import the source Hive metastore to the target database.
```
mysql -hX.X.X.X -uroot -pXXXX hivemetastore < hivemetastore-src.sql  
# `X.X.X.X` is the IP address of the database server  
# `XXXX` is the database password  
# If the database user is not `root`, use the correct username  
# `hivemetastor` is the Hive metastore name 
```
8. Upgrade the Hive metadata.
If the versions of the target and source Hive databases are the same, you can skip this step; otherwise, query the Hive version in the source and target clusters, respectively.
```
hive --service version 
```
The Hive upgrade script is stored in the `/usr/local/service/hive/scripts/metastore/upgrade/mysql/` directory.

 Hive does not support upgrade across major versions. For example, if you want to upgrade Hive from 1.2 to 2.3.0, perform the following operations in sequence:
```
upgrade-1.2.0-to-2.0.0.mysql.sql -> upgrade-2.0.0-to-2.1.0.mysql.sql -> upgrade-2.1.0-to-2.2.0.mysql.sql -> upgrade-2.2.0-to-2.3.0.mysql.sql
```
The main operations in the upgrade script are creating tables, adding fields, and modifying content. If a table or field already exists, the exception for table or field existence can be ignored during the upgrade. For example, you can upgrade Hive from 2.3.3 to 3.1.1 as follows:
```
mysql> source upgrade-2.3.0-to-3.0.0.mysql.sql;  
mysql> source upgrade-3.0.0-to-3.1.0.mysql.sql;  
```
9. Modify the ZooKeeper address of the Phoenix table in the target Hive metadata.
If there is a Phoenix table in the source Hive database, run the following query statement to get the `phoenix.zookeeper.quorum` configuration of the Phoenix table.
```
mysql> SELECT PARAM_VALUE from TABLE_PARAMS where PARAM_KEY = 'phoenix.zookeeper.quorum';  
+--------------------------------------------------+    
| PARAM_VALUE |    
+--------------------------------------------------+    
| 172.17.64.57,172.17.64.78,172.17.64.54 |     
+--------------------------------------------------+  
```
View the ZooKeeper address of the target cluster, i.e., the value specified in `hbase.zookeeper.quorum` of the `hive-site.xml` configuration file.
```
<property>  
    <name>hbase.zookeeper.quorum</name>  
    <value>172.17.64.98:2181,172.17.64.112:2181,172.17.64.223:2181</value>  
</property>  
```
Modify the ZooKeeper address of the Phoenix table in the target Hive metadata to that of the target cluster.
```
mysql> UPDATE TABLE_PARAMS set PARAM_VALUE  = '172.17.64.98,172.17.64.112,172.17.64.223' where PARAM_KEY = 'phoenix.zookeeper.quorum';    
```
10. Start the MetaStore, HiveServer2, and WebHcataLog services of the target Hive database.
11. You can run simple Hive SQL query statements to check the migration result.

 
