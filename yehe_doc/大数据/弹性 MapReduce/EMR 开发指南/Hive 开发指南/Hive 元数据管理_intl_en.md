When you choose to deploy the Hive component, there are two storage methods for Hive metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster (default method) or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in the associated database and will not be deleted when the cluster is terminated.

In the former case, a MetaDB instance is automatically purchased to store Hive metadata, alongside metadata of other components. The MetaDB instance will be terminated too when the cluster is terminated. If you need to retain the metadata, please go to the TencentDB console and save it manually in advance.
>!
>1. Hive metadata is stored together with the metadata of Druid, Superset, Hue, Ranger, Oozie, and Presto.  
>2. A MetaDB instance needs to be purchased separately for the cluster as the metadatabase.
>3. The MetaDB instance will be terminated when the cluster is terminated, i.e., the metadata stored in it will be deleted.

## Associating with EMR-MetaDB for Hive Metadata Sharing
When a cluster is created, the system will pull an MetaDB instance available in the cloud as the Hive metadatabase, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Moreover, Hive metadata will not be deleted when the cluster is terminated.
> !
>1. The ID of the available MetaDB instance is the ID of an existing MetaDB instance in the EMR cluster under the same account.
>2. If one or more components among Hue, Ranger, Oozie, Druid, and Superset are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
>3. To terminate the associated EMR-MetaDB instance, you need to go to the TencentDB console to do so. Hive metadatabases cannot be recovered once terminated.
>4. Make sure that the associated EMR-MetaDB instance is in the same network as the newly created cluster.
>
![](https://main.qcloudimg.com/raw/ea80da978befc52ce178f6dcd6efc549.png)![](https://main.qcloudimg.com/raw/e247c5d9419bfc87444546ffe8718eac.png)

## Associating with Self-built MySQL Database for Hive Metadata Sharing
You can associate with your local self-built MySQL database to store Hive metadata, so you don't need to purchase a MetaDB instance separately, which helps reduce your storage costs. Please enter the address beginning with "jdbc:mysql://", username, and login password of the database correctly and make sure that the database can be connected with the cluster.
> !
>1. Make sure that the self-built database is in the same network as the EMR cluster.
>2. Enter the username and password of the database correctly.
>3. If one or more components among Hue, Ranger, Oozie, Druid, and Superset are selected, a MetaDB instance will be automatically purchased to store the metadata of such components other than Hive.
>4. Make sure that the Hive metadata version in the custom database is not below the Hive version in the new cluster.
>
![](https://main.qcloudimg.com/raw/782ec9f2053ecbac9bb49590dd2849d0.png)![](https://main.qcloudimg.com/raw/80832e95e7603c83e416d279d5715ea6.png)

## Fixing Exception in Associating Self-built Metadatabase with Hive
If **Associated self-built MySQL** is selected when the EMR cluster is created, and the self-built MySQL instance contains no metadata of Hive, Hive process exception will occur.
### Problem recurring
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UUHR194_%E5%9B%BD%E9%99%8510.png)
### Solution
For Hive metadata which contains no data, operate as follows:
>? Use your real ${ip}, ${port}, and ${database} in the operation.
>
1. Stop `hs2` and `metastore` of Hive in the console.
2. Modify and deliver `hive-site.xml proto-hive-site.xml` of Hive.
Configuration item: javax.jdo.option.ConnectionURL
```
jdbc:mysql://${ip}:${port}/${database}?useSSL=false&amp;createDatabaseIfNotExist=true&amp;characterEncodin
g=UTF-8
```
3. Delete the database in the CDB instance:
```
drop database ${database};
```
4. For a Hadoop user, run the following command:
```
/usr/local/service/hive/bin/schematool -dbType mysql -initSchema
```
5. Start `hs2` and `metastore` of Hive in the console.
6. Check whether Hive can be properly accessed.
In case of character exception, run the following command on the CDB instance:
```
alter database ${database} character set latin1;
flush privileges;
```
