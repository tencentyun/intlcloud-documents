## Overview

GooseFS’s metadata management feature can be used to manage structured data. It manages database tables of upper-layer computing applications such as Spark SQL, Hive, and Presto. You can connect it to the underlying Hive Metastore. Metadata management allows SQL engines to read specified data and speeds up data access when the data volume is high.

![](https://main.qcloudimg.com/raw/c3616ae043e36bc5ea462fa960e20fbb.png)        

GooseFS’s metadata management introduces the following features:

- Describe metadata. GooseFS Catalog supports caching metadata from a remote Hive Metastore. If SQL engines (such as Spark SQL, Hive, and SQL Presto) are querying data, GooseFS Catalog’s metadata caching service can determine the target data’s size, location, and structure the way Hive Metastore does.
- Cache table-level data in advance. GooseFS Catalog detects the mapping relationship between tables and their storage paths and thus can cache table or partition level data in advance to speed up data access.
- Unify metadata queries from multiple storage services. You can use GooseFS Catalog to run upper-layer computing applications and speed up access to various underlying storage services. Moreover, GooseFS Catalog supports cross-storage metadata queries. You only need to enable Catalog on one GooseFS client and can query data stored in different storage systems such as HDFS, COS, and CHDFS.

## How It Works

GooseFS metadata management is implemented with `goosefs table` commands shown below, which can be used to attach/detach databases, query database/table information, load/free data, and more.

```plaintext
$ goosefs table
Usage: goosefs table [generic options]
	 [attachdb [-o|--option <key=value>] [--db <goosefs db name>] [--ignore-sync-errors] <udb type> <udb connection uri> <udb db name>]
	 [detachdb <db name>]                                      
	 [free <dbName> <tableName> [-p|--partition <partitionSpec>]]
	 [load <dbName> <tableName> [-g|--greedy] [--replication <num>] [-p|--partition <partitionSpec>]]
	 [ls [<db name> [<table name>]]]                           
	 [stat <dbName> <tableName>]                               
	 [sync <db name>]                                          
```

The commands are described as follows:

- attachdb: attaches a remote database to GooseFS. Currently, only Hive Metastore is supported.
- detachdb: detaches a database from GooseFS.
- free: frees data cache of a specified DB.Table (partition-level is supported).
- load: loads data of a specified DB.Table (partition-level is supported). You can use `replication` to specify the number of replicas to cache.
- ls: lists metadata of a DB or DB.Table.
- stat: queries the statistics on a specified DB.Table, including the number of files, total size, and the percentage cached.
- sync: syncs data of a specified database.
- transform: transforms a table in a specified database into a new table.
- transformStatus: queries table transforming status.

### 1. Attaching a database

You need to attach the database to GooseFS before loading the table data. Run the following command to attach the database `goosefs_db_demo` from `metastore_host:port` to GooseFS and name this database `test_db` in GooseFS:

```plaintext
$ goosefs table attachdb --db test_db hive thrift://metastore_host:port goosefs_db_demo

response of attachdb
```

>! You can replace `metastore_host:port` with any valid and connectable Hive Metastore address.
>

### 2. Viewing table information

After the database is attached, run the `ls` command to view the attached database and table information. The following command shows how to query information about the `web_page` table in `test_db`:

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
   gfs://metastore_host:port/myiNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://metastore_host:port/myNamespace/3000/web_page
   }
)
```


### 3. Loading table data

Once the data loading command is delivered, an async job will be initiated in the backend, and GooseFS will return the job ID after the job is started. You can run the `job stat <ID>` command to view the running status of the job, or run the `table stat` command to view the percentage cached. The data loading command is as follows:

```plaintext
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```


### 4. Viewing statistics on table loading

Run the `job stat` command to view the execution progress of the table loading job. If the status is `COMPLETED`, the table has been loaded successfully. If the status is `FAILED`, you can view the logs in `master.log` to troubleshoot.

```plaintext
$ goosefs job stat 1615966078836
COMPLETED
```

When the table is loaded, run the `stat` command to view the statistics on the table.

```plaintext
$ goosefs table stat test_db web_page
detail
```


### 5. Freeing a table

Run the following table to free the cache of a specified table from GooseFS:

```plaintext
$ goosefs table free test_db web_page
detail
```


### 6. Detaching the database

Run the following command to detach a specified database from GooseFS:

```plaintext
$ goosefs table detachdb test_db
detail
```
