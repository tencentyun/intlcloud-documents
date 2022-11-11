# Overview

The [CosN](https://intl.cloud.tencent.com/document/product/436/6884) plugin implements a COS-based standard Hadoop file system to help integrate big data computing frameworks (such as Hadoop, Spark, and Tez) with COS. You can use CosN to read data stored in COS. If you are already using CosN to access COS, you can use GooseFS’s client-based path mapping method to access GooseFS with the CosN schema without modifying the definition of the current Hive table to facilitate the comparison tests of GooseFS features/performance.

The mapping between CosN Schema and GooseFS Schema is described as follows:

Assuming that the UFS path of the namespace warehouse is `cosn://examplebucket-1250000000/data/warehouse/`, the CosN-to-GooseFS path mapping will be as follows:
```plaintext
cosn://examplebucket-1250000000/data/warehouse -> /warehouse/
cosn://examplebucket-1250000000/data/warehouse/folder/test.txt ->/warehouse/folder/test.txt
```
GooseFS-to-CosN path mapping:
```plaintext
/warehouse ->cosn://examplebucket-1250000000/data/warehouse/
/warehouse/ -> cosn://examplebucket-1250000000/data/warehouse/
/warehouse/folder/test.txt -> cosn://examplebucket-1250000000/data/warehouse/folder/test.txt
```
 
The CosN schema maintains the mapping between GooseFS and UFS CosN paths on the client, and converts CosN-path requests to GooseFS-path requests. The mapping is refreshed periodically. You can modify the refresh interval (default: 60s) with `goosefs.client.namespace.refresh.interval` in the GooseFS configuration file `goosefs-site.properties`.

>! If the accessed CosN path cannot be converted into a GooseFS path, the corresponding Hadoop API call will throw an exception.
>

## Operation Examples

This example shows how to access GooseFS using Schema gfs:// and Schema cosn:// on the Hadoop command-line tool and Hive.

### 1. Prepare the data and computing cluster

- [Creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309) for testing purposes.
- [Create a folder](https://intl.cloud.tencent.com/document/product/436/13329) named `ml-100k` in the root directory of the bucket.
- Download the `ml-100k` dataset from [Grouplens](https://grouplens.org/datasets/movielens/100k/) and upload the `u.user` file to `<Bucket root directory>/ml-100k`.
- Purchase an EMR cluster and configure the HIVE component by referring to the EMR documentation.

### 2. Configure the environment

i. Put the GooseFS client package `goosefs-1.0.0-client.jar` in the `share/hadoop/common/lib/` directory.
```plaintext
 cp goosefs-1.0.0-client.jar  hadoop/share/hadoop/common/lib/
```
 >! The configuration update and JAR package should be synced to all nodes in the cluster.
 >
ii. Modify the Hadoop configuration file `etc/hadoop/core-site.xml` to specify the GooseFS class implementation.
```plaintext
<property>
  <name>fs.AbstractFileSystem.gfs.impl</name>
  <value>com.qcloud.cos.goosefs.hadoop.GooseFileSystem</value>
</property>
<property>
  <name>fs.gfs.impl</name>
  <value>com.qcloud.cos.goosefs.hadoop.FileSystem</value>
</property>
```
iii. Run the following Hadoop command to check whether you can access GooseFS using the `gfs://` Schema, where &lt;MASTER_IP> is the IP of the master.
```plaintext
hadoop fs -ls gfs://<MASTER_IP>:9200/
```
iv. Put the JAR package of the GooseFS client to the `hive/auxlib/` directory for Hive to load it.
```plaintext
cp goosefs-1.0.0-client.jar  hive/auxlib/
```
v. Run the following command to create a namespace whose UFS schema is CosN and list the namespace. Replace `examplebucket-1250000000` with your actual COS bucket, and `SecretId` and `SecretKey` with your actual key information.
```plaintext
goosefs ns create ml-100k cosn://examplebucket-1250000000/ml-100k  --secret fs.cosn.userinfo.secretId=SecretId --secret fs.cosn.userinfo.secretKey=SecretKey--attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider
goosefs ns ls
```

### 3. Create a GooseFS Schema and query data

Run the following commands:

```plaintext
create database goosefs_test;

use goosefs_test;
CREATE TABLE u_user_gfs (
userid INT,
age INT,
gender CHAR(1),
occupation STRING,
zipcode STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE
LOCATION 'gfs://<MASTER_IP>:<MASTER_PORT>/ml-100k';

select sum(age) from u_user_gfs;
```


### 4. Create CosN Schema and query data

Run the following commands:

```plaintext
CREATE TABLE u_user_cosn (
userid INT,
age INT,
gender CHAR(1),
occupation STRING,
zipcode STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE
LOCATION 'cosn://examplebucket-1250000000/ml-100k';

select sum(age) from u_user_cosn;
```

### 5. Modify the CosN implementation to GooseFS-compatible

Modify `hadoop/etc/hadoop/core-site.xml`:

```plaintext
 <property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>com.qcloud.cos.goosefs.hadoop.CosN</value>
    </property>
    <property>
        <name>fs.cosn.impl</name>
        <value>com.qcloud.cos.goosefs.hadoop.CosNFileSystem</value>
    </property>
```

Run the Hadoop command below. If the path cannot be converted into a GooseFS path, an error message will be displayed in the command output.

```plaintext
hadoop fs -ls  cosn://examplebucket-1250000000/ml-100k/

Found 1 items
-rw-rw-rw-   0 hadoop hadoop      22628 2021-07-02 15:27 cosn://examplebucket-1250000000/ml-100k/u.user
 
hadoop fs -ls cosn://examplebucket-1250000000/unknow-path
ls: Failed to convert ufs path cosn://examplebucket-1250000000/unknow-path to GooseFs path, check if namespace mounted 
```

Run the Hive query language again:

```plaintext
select sum(age) from u_user_cosn;
```
