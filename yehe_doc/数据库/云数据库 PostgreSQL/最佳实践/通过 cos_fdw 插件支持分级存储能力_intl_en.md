## Background
As the core component for data storage and processing, a database will have an increasing data volume as the business develops. Some historical or archived data may exist over time or because of the business design logic. Such data is seldom accessed by the business but cannot be deleted, as it may be used in some scenarios. To improve the database's processing performance, you need to store such data in a cold storage class.

For databases, it is very important to store as much data as possible and provide better unified data processing APIs. For such user requirements, TencentDB for PostgreSQL offers a tiered data storage scheme. Its core principle is to offer storage media at different costs for your choice. For example, you can store cold data in a storage class with a lower performance but at lower costs and store hot data in high-performance SSDs at higher costs. This scheme guarantees smooth operations of your business and reduces the storage costs, making it extremely cost-effective.

## Overview
COS is an object storage service provided by Tencent Cloud. Currently, tiered storage is mainly implemented by connecting to and parsing COS data through the cos_fdw extension.
You can use the cos_fdw extension to load COS data into TencentDB for PostgreSQL tables and access COS data just like a regular table, thereby implementing hot/cold data separation. You don't need to care about how different storage media are accessed. You only need to configure COS data files to TencentDB for PostgreSQL.

## Solution Strengths
- **Unified engine**: It provides multiple types of storage media with no need to modify the code at the business layer. You can implement unified access directly over the PostgreSQL protocol.
- **Lower costs**: Compared with high-performance SSDs, its overall costs are 86.25% lower.
- **Ease of use**: You only need to export the source data to a CSV file in COS and create a foreign table in TencentDB for PostgreSQL based on the extension. Then, you can use the foreign table just like the original table.
- **Unlimited storage**: COS offers an unlimited storage capacity. You can dynamically store data as needed without worrying about the capacity.
- **Support for joined table queries**: You can query joined tables in multiple storage media and join tables across partitions. As such operations require a unified data fusion node, they cannot be directly performed in other databases.

## Supported Versions
Currently, tiered storage is supported for the following TencentDB for PostgreSQL versions:
- PostgreSQL 10
- PostgreSQL 11
- PostgreSQL 12
- PostgreSQL 13
- PostgreSQL 14

## Using cos_fdw
Use cos_fdw in the following steps:
1. Export the data.
2. Upload the data to COS.
3. Create the cos_fdw extension.
4. Create a foreign server.
5. Create a foreign table.
6. Query the foreign table.

## Initializing Environment
First, you need to apply for a relay server, such as a CVM instance, with a low specification in the same region and AZ as the database and COS bucket.
- Recommended OS: CentOS 7.
1. Install the PostgreSQL client as instructed in [Linux downloads (Red Hat family)](https://www.postgresql.org/download/linux/redhat/).
```
sudo yum install -y 
https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-
x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo yum install -y postgresql13
```
2. After the installation is completed, run the `psql` command to access the database and check whether the client is installed successfully:
```
psql -Uroot -p 5432 -h 10.x.x.8 -d postgres
Password for user root: 
psql (13.6, server 13.3)
Type "help" for help.

postgres=>
```
3. After the PostgreSQL client is installed, mount COS. You can use COSFS to mount COS to the server, which eliminates the need to use a larger CVM instance for data dumping and upload. For more information, see [COSFS](https://intl.cloud.tencent.com/document/product/436/6883).
4. Run the following command to install dependency packages for your current environment:
```
sudo yum install libxml2-devel libcurl-devel -y
```
5. Download the COSFS installation package from [GitHub](https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs-1.0.19-centos7.0.x86_64.rpm).
6. After the download is completed, upload the package to the server and run the following command to install COSFS:
```
rpm -ivh cosfs-1.0.19-centos7.0.x86_64.rpm
```
>!If dependency packages are installed, but COSFS still cannot be installed successfully, add the `--force` parameter to the command to forcibly install it.
7. After installing COSFS, run the following command to mount the COS bucket to the relay server.
```
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.c
om -odbglevel=info -oallow_other
```
 - `BucketName-APPID` is the format of the bucket name.
 - `SecretId` and `SecretKey` are the key information.
8. After mounting, go to the mounted directory and copy a file to check whether the mounting succeeds. You can also run `df -h` to view the mounting status.
```
[root@VM-4-17-centos ~]# df -h
Filesystem Size Used Avail Use% Mounted on
devtmpfs 1.9G 0 1.9G 0% /dev
tmpfs 1.9G 0 1.9G 0% /dev/shm
tmpfs 1.9G 472K 1.9G 1% /run
tmpfs 1.9G 0 1.9G 0% /sys/fs/cgroup
/dev/vda1 50G 3.0G 44G 7% /
tmpfs 379M 0 379M 0% /run/user/0
cosfs 256T 0 256T 0% /mnt/pgstorage
```

## Exporting Data
After mounting is completed, export the data.
If the `sensor_log` table exists, it needs to be in the following structure:
```
CREATE TABLE sensor_log (
 sensor_log_id SERIAL PRIMARY KEY,
 location VARCHAR NOT NULL,
 reading BIGINT NOT NULL,
 reading_date TIMESTAMP NOT NULL
);
CREATE INDEX idx_sensor_log_location ON sensor_log (location);
CREATE INDEX idx_sensor_log_date ON sensor_log (reading_date);
insert into sensor_log(location,reading,reading_date) values('38c-
1401',293857,current_timestamp);
insert into sensor_log(location,reading,reading_date) values('38c-
1402',293858,current_timestamp);
insert into sensor_log(location,reading,reading_date) values('34c-
1401',293859,current_timestamp);
insert into sensor_log(location,reading,reading_date) values('18c-
1401',2938510,current_timestamp);
```

If you use psql to export the data, follow the steps below (do not carry the header during export):
**Export the entire table**:
```
psql -U root -p 5432 -h 10.0.4.8 -d hehe -c \COPY sensor_log 
(sensor_log_id,location, reading,reading_date) TO '/mnt/xxx/sensor_log.csv' WITH 
csv;
```

**Export specified data (for scenarios such as data filtering, multi-table join, and view)**:
```
psql -U root -p 5432 -h 10.0.4.8 -d hehe -c '\COPY (select * from sensor_log 
where location='18c-1401') TO '/mnt/pgstorage/sensor_log.csv' WITH csv;'
```
After the above statement is executed, you can find the exported file in the corresponding directory in the COS bucket.
The CSV file exported to COS doesn't need to contain column names.

## Creating Extension
The cos_fdw extension will encrypt the secret ID and secret key of COS. The encryption algorithm relies on the pgcrypto extension. Therefore, you need to install pgcrypto first.
```
CREATE EXTENSION pgcrypto;
CREATE EXTENSION cos_fdw;
```

## Creating Foreign Server
```
CREATE SERVER cos_server FOREIGN DATA WRAPPER cos_fdw OPTIONS(
 host 'xxxxxx.cos.ap-nanjing.myqcloud.com',
 bucket 'xxxxxxxx',
 id 'xxxxxxxx',
 key 'xxxxxxxxxx'
);
```

>!
>- The domain name configured in `host` is the access address of the COS bucket. The address doesn't need to contain the `http` or `https` prefix as the protocol.
>- `id` and `key` of the foreign server are sensitive information, which will be encrypted and stored by cos_fdw. Different instances use different keys to maximize the user information protection. You can run `SELECT * FROM pg_foreign_server;` to view the information.

## Creating COS Foreign Table
```
CREATE FOREIGN TABLE test_csv (
 word1 text OPTIONS (force_not_null 'true'),
 word2 text OPTIONS (force_not_null 'off') ) SERVER cos_server OPTIONS (
 filepath '/test.csv',
 format 'csv',
 null 'NULL'
);
```
`cos_fdw` allows you to map multiple COS files to the same foreign table. To do so, enter multiple filenames in the `filepath` parameter and separate them with commas (do not add spaces).

```
CREATE FOREIGN TABLE multi_csv (
 word1 text OPTIONS (force_not_null 'true'),
 word2 text OPTIONS (force_not_null 'off') ) SERVER cos_server OPTIONS (
 filepath '/a.csv,/b.csv,/c.csv.2',
 format 'csv',
 null 'NULL'
);
```

## Querying Foreign Table
### Scheduling query plan
cos_fdw can estimate the size of foreign files for scheduling the query plan. For a foreign table mapped to multiple COS files, cos_fdw can print out the size of each file and calculate the total size of all files.
```
-- Single file
postgres=# EXPLAIN SELECT * FROM test_csv;
 QUERY PLAN 
-----------------------------------------------------------------
--------------
Foreign Scan on test_csv (cost=0.00..1.10 rows=1 width=128)
 Foreign COS Url: https://xxxxxxx.cos.ap-nanjing.myqcloud.com
 Foreign COS File Path: /test_csv.csv
 Foreign each COS File Size(Bytes): 86
 Foreign total COS File Size(Bytes): 86
(5 rows)
-- Multiple files
postgres=# EXPLAIN SELECT * FROM multi_csv;
 QUERY PLAN 
-----------------------------------------------------------------
---------------
Foreign Scan on multi_csv (cost=0.00..1.20 rows=2 width=128)
 Foreign COS Url: https://xxxxxxxxxx.cos.ap-nanjing.myqcloud.com
 Foreign COS File Path: /a.csv,/b.csv,/c.csv.2
 Foreign each COS File Size(Bytes): 15,172,86
 Foreign total COS File Size(Bytes): 273
(5 rows)
```

### Querying data
```
postgres=# SELECT * FROM test_csv;
word1 | word2 | word3 | word4 
-------+-------+-------+-------
AAA | aaa | 123 |
XYZ | xyz | | 321
NULL | | |
NULL | | |
ABC | abc | | (5 rows)
```

### Importing data from foreign table to local table
You can use statements similar to `insert into ... select * from ...;` to import data from a foreign table to a local table.
```
postgres=# CREATE TABLE local_test_csv (
postgres(# a text,
postgres(# b text,
postgres(# c text,
postgres(# d text
postgres(# );
CREATE TABLE
postgres=# INSERT INTO local_test_csv SELECT * FROM test_csv;
INSERT 0 5
postgres=# SELECT * FROM local_test_csv;
 a | b | c | d 
------+-----+-----+-----
AAA | aaa | 123 |
XYZ | xyz | | 321
NULL | | |
NULL | | |
ABC | abc | | (5 rows)
```

### Querying partitioned table
```
postgres=# CREATE TABLE pt (a int, b text) partition by list (a);
CREATE TABLE
postgres=# CREATE FOREIGN TABLE p1 partition of pt for values in (1) SERVER
cos_server
postgres-# OPTIONS (format 'csv', filepath '/list1.csv', delimiter ',');
CREATE FOREIGN TABLE
postgres=# CREATE TABLE p2 partition of pt for values in (2);
CREATE TABLE
-- Partitioned tables can be queried
postgres=# SELECT tableoid::regclass, * FROM pt;
tableoid | a | b 
----------+---+-----
p1 | 1 | foo
p1 | 1 | bar
(2 rows)
postgres=# SELECT tableoid::regclass, * FROM p1;
tableoid | a | b 
----------+---+-----
p1 | 1 | foo
p1 | 1 | bar
(2 rows)
postgres=# SELECT tableoid::regclass, * FROM p2;
tableoid | a | b 
----------+---+---
(0 rows)
-- Currently, data cannot be written to foreign tables
postgres=# INSERT INTO pt VALUES (1, 'xyzzy'); -- ERROR
ERROR: cannot route inserted tuples to a foreign table
-- As local tables are not affected, data can be written to local partitioned tables normally.
postgres=# INSERT INTO pt VALUES (2, 'xyzzy');
INSERT 0 1
postgres=# SELECT tableoid::regclass, * FROM pt;
tableoid | a | b 
----------+---+-------
p1 | 1 | foo
p1 | 1 | bar
p2 | 2 | xyzzy
(3 rows)
postgres=# SELECT tableoid::regclass, * FROM p1;
tableoid | a | b 
----------+---+-----
p1 | 1 | foo
p1 | 1 | bar
(2 rows)
postgres=# SELECT tableoid::regclass, * FROM p2;
tableoid | a | b 
----------+---+-------
p2 | 2 | xyzzy
(1 row)
```

## Dropping Extension
```
DROP EXTENSION cos_fdw;
```

## Parameters
**`CERATE SERVER` parameters**

| Parameter | Description |
|---------|---------|
| host | Address for accessing COS over the private network. Note that `host` cannot contain the `http` or `https` prefix. |
| bucket | Bucket name in the format of `BucketName-APPID` |
| id | Account secret ID |
| key | Account secret key |

**`CREATE FOREIGN TABLE` parameters**

| Parameter | Description |
|---------|---------|
| filepath | Sample |
| format | Data format, which currently can only be CSV. |
| delimiter | Data delimiter |
| quote | Data quote character |
| escape | Data escape character |
| encoding | Data encoding |
| null | Specifies that the column matching the corresponding string is `null`. For example, `null 'NULL'` indicates to specify the string of the column value 'NULL' to `null`  |
| force_not_null | Specifies that the column's value should not match an empty string. For example, `force_not_null 'id'` indicates that if the value of the `id` column is empty, the value queried from the foreign table is an empty string but not `null`. |
| force_null | Specifies that the column's value matches an empty string. For example, `force_null 'id'` indicates that if the value of the `id` column is empty, the value queried from the foreign table is `null`. |

## Error Handling
When a data request sent by cos_fdw to COS times out, the following will be displayed:
- code: HTTP status code of the abnormal request.
- HTTP header: Error information. For more information on the format, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the `x-cos-request-id` for assistance. If the field is empty, the request failed to be sent to COS.

```
• postgres=# SELECT * FROM test_csv; • ERROR: COS api return error. • DETAIL: COS api http status:403
• HTTP/1.1 403 Forbidden
• Content-Type: application/xml
• Content-Length: 0 • Connection: keep-alive
• Date: Thu, 07 Apr 2022 09:00:22 GMT
• Server: tencent-cos
• x-cos-request-id: NjI0ZWE4MjZfNDc1NGU0MDlfMjI3ZTJfMTI3YTJjMWM= 
• x-cos-trace-id:
OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OTBjYzE2MjAxN2M1MzJiOTdkZjMxMDVlYTZjN2FiMmI0MWMyZGYxMDAyZmVmMjNkZDQ5NGViMDhiZWJkOTE2YzI=
```

