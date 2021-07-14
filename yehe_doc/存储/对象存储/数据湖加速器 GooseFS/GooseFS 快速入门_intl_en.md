
This document describes how to quickly employ GooseFS on a local device, perform debugging, and use COS as remote storage.


## Prerequisites

Before using GooseFS, you need to:

1. Create a bucket in COS as remote storage. For detailed directions, please see [Getting Started](https://intl.cloud.tencent.com/document/product/436/32955).
2. Install [Java 8 or a later version](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html).
3. Install [SSH](https://www.ssh.com/ssh/), ensure that you can connect to the LocalHost using SSH, and log in remotely.

## Downloading and Configuring GooseFS

1. Download the GooseFS installation package from the repository.
2. Run the following command to decompress the installation package:
```plaintext
tar -zxvf goosefs-1.0.0-bin.tar.gz
cd goosefs-1.0.0
```
3. After the decompression, the GooseFS installation package, source files, and Java binary files will be stored in the `goosefs-1.0.0` folder. This document includes them from `${GOOSEFS_HOME}`.
4. Create the `conf/goosefs-site.properties` configuration file in `${GOOSEFS_HOME}/conf`. You can use a built-in configuration template.
```plaintext
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
5. Set `goosefs.master.hostname` to `localhost` in `conf/goosefs-site.properties`.
```plaintext
$ echo"goosefs.master.hostname=localhost">> conf/goosefs-site.properties
```

## Running GooseFS 

1. Before running GooseFS, run the following command to check the local system environment to ensure that GooseFS can run properly:
```plaintext
$ goosefs validateEnv local
```
 >? The command above allows you to view the running status of GooseFS.
 >
2. Run the command below to format GooseFS before you run it. This command clears the logs of GooseFS and files stored in the `worker` directory.
```plaintext
$ goosefs format
```
3. Run the command below to run GooseFS. By default, a master and a worker will be enabled.
```plaintext
$ ./bin/goosefs-start.sh local SudoMount
```
After the command above is executed, you can access http://localhost:9201 and http://localhost:9204 to view the running status of the master and the worker, respectively.

## Using GooseFS to Mount COS
1. Create a namespace and mount it to COS:
```plaintext
$ goosefs ns create myNamespace cosn://bucketName-125xxxxxx/ 3TB
--option fs.cosn.userinfo.secretId=AKIDxxxxxxxxxxxxxx \
--option fs.cosn.userinfo.secretKey=xxxxxxxxxxxxxxxxx \
--option fs.cosn.bucket.region=ap-guangzhou \
```
>! When creating the namespace, the `–-option` parameter, as well as all required parameters of Hadoop-COS (COSN), must be specified. For more information about the parameters required, please see [Hadoop](https://intl.cloud.tencent.com/document/product/436/6884). When you create the namespace, if there is no read/write permission (rPolicy/wPolicy) specified, the read/write type specified in the configuration file, or the default value (CACHE/CACHE_THROUGH) will be used.
>
2. After the mount succeeds, you can run the `ls` command to list all namespaces created in the cluster as follows:
```plaintext
$ goosefs ns list
namespace      mountPoint       ufsPath                      creationTime                wPolicy      rPolicy     TTL   ttlAction
myNamespace    /myNamespace   cosn://bucketName-125xxxxxx/3TB  03-11-2021 11:43:06:239      CACHE_THROUGH   CACHE        -1      DELETE
```
3. To view information about a specific namespace, run the following command:
```plaintext
$ goosefs ns stat myNamespace

NamespaceStatus{name=myNamespace, path=/myNamespace, ttlTime=-1, ttlAction=DELETE, ufsPath=cosn://bucketName-125xxxxxx/3TB, creationTimeMs=1615434186076, lastModificationTimeMs=1615436308143, lastAccessTimeMs=1615436308143, persistenceState=PERSISTED, mountPoint=true, mountId=4948824396519771065, acl=user::rwx,group::rwx,other::rwx, defaultAcl=, owner=user1, group=user1, mode=511, writePolicy=CACHE_THROUGH, readPolicy=CACHE}
```

Information recorded in the metadata is as follows:

| NO. | Parameter | Description |
| ---- | ---------------------- | ----- |
| 1    | name  | Name of the namespace |
| 2    | path | Path of the namespace in GooseFS |
| 3    | ttlTime | TTL period of files and directories in the namespace |
| 4    | ttlAction | TTL action to handle files and directories in the namespace. Valid values: `FREE` (default), `DELETE` |
| 5    | ufsPath | Mount path of the namespace in the UFS |
| 6    | creationTimeMs | Time when the namespace is created, in milliseconds |
| 7    | lastModificationTimeMs | Time when files or directories in the namespace is last modified, in milliseconds |
| 8    | persistenceState | Persistence state of the namespace |
| 9    | mountPoint             | Whether the namespace is a mount target. The value is fixed to `true`. |
| 10   | mountId  | Mount target ID of the namespace |
| 11   | acl | ACL of the namespace |
| 12   | defaultAcl | Default ACL of the namespace |
| 13   | owner | Owner of the namespace |
| 14   | group | Group where the namespace owner belongs |
| 15   | mode | POSIX permission of the namespace |
| 16   | writePolicy | Write policy for the namespace |
| 17   | readPolicy | Read policy for the namespace |


## Restoring table data to GooseFS

1. You can restore hive table data to GooseFS. Before the restoration, attach the database to GooseFS using the following command:
```plaintext
$ goosefs table attachdb --db test_db hive thrift://
172.16.16.22:7004 test_for_demo
```
>! Replace `thrift` in the command with the actual Hive Metastore address.
>
2. After the database is attached, run the `ls` command to view information about the attached database and table:
```plaintext
$ goosefs table ls test_db web_page

OWNER: hadoop
DBNAME.TABLENAME: testdb.web_page (
   wp_web_page_sk bigint,
   wp_web_page_id string,
   wp_rec_start_date string,
   wp_rec_end_date string,
   wp_creation_date_sk bigint,
   wp_access_date_sk bigint,
   wp_autogen_flag string,
   wp_customer_sk bigint,
   wp_url string,
   wp_type string,
   wp_char_count int,
   wp_link_count int,
   wp_image_count int,
   wp_max_ad_count int,
)
PARTITIONED BY (
)
LOCATION (
   gfs://172.16.16.22:9200/myNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://172.16.16.22:9200/myNamespace/3000/web_page
   }
)
```
3. Run the `load` command to restore table data:
```plaintext
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```

Restoring table data is asynchronous. Therefore, a job ID will be returned. You can run the `goosefs job stat &lt;Job Id>` command to view the restoration progress. When the status becomes "COMPLETED", the restoration succeeds.

## Using GooseFS for Uploads/Downloads

1. GooseFS supports most file system−related commands. You can run the following command to view the supported commands:
```plaintext
$ goosefs fs
```
2. Run the `ls` command to list files in GooseFS. The following example lists all files in the root directory:
```plaintext
$ goosefs fs ls /
```
3. Run the `copyFromLocal` command to copy a local file to GooseFS:
```plaintext
$ goosefs fs copyFromLocal LICENSE /LICENSE
Copied LICENSE to /LICENSE
$ goosefs fs ls /LICENSE
-rw-r--r--  hadoop         supergroup               20798       NOT_PERSISTED 03-26-2021 16:49:37:215   0% /LICENSE
```
4. Run the `cat` command to view the file content:
```plaintext
$ goosefs fs cat /LICENSE                                                                         
Apache License
Version 2.0, January 2004
http://www.apache.org/licenses/
TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
...
```
5. By default, GooseFS uses the local disk as the underlying file system. The default file system path is `./underFSStorage`. You can run the `persist` command to store files to the local system persistently as follows:
```plaintext
$ goosefs fs persist /LICENSE
persisted file /LICENSE with size 26847
```

## Using GooseFS to Accelerate Uploads/Downloads

1. Check the file status to determine whether a file is cached. The file status `PERSISTED` indicates that the file is in the memory, and `NOT_PERSISTED` indicates not.
```plaintext
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 NOT_PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
```
2. Count how many times “tencent” appeared in the file and calculate the time consumed:
```plaintext
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m22.857s
user	0m7.557s
sys	0m1.181s
```
3. Caching data in memory can effectively speed up queries. An example is as follows:
```plaintext
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m1.917s
user	0m2.306s
sys	    0m0.243s
```

The data above shows that the system delay is reduced from 1.181s to 0.243s, achieving a 10-times improvement.

## Shutting Down GooseFS

Run the following command to shut down GooseFS:
```plaintext
$ ./bin/goosefs-stop.sh local
```

