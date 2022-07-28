## Background
In data warehouse construction, Hive is usually used to process the raw data (at the petabyte level), perform time-consuming ETL jobs, and hand over the results (at the terabyte level) to a quasi-real-time computing engine such as CDWPG to connect BI tools and present reports in quasi real time.

This document describes how to import data from Hive on EMR to CDWPG via COS.

## Directions
>!
>- CDWPG supports only CSV and GZIP but not ORC and Parquet formats.
>- The efficiency of importing COS data to CDWPG depends on the number of files, which is recommended to be N times the number of compute nodes in CDWPG.

1. Enable EMR's capability to read and write COS data.
  First, you need to ensure that EMR is able to read and write COS data. You can click **Enable** COS when creating an EMR instance.
  

2. Create a Hive local table and write data into it.
```
create table hive_local_table(c1 int, c2 string, c3 int, c4 string);
insert into hive_local_table values(1001, 'c2', 99, 'c4'),(1002, 'c2', 100, 'c4'),(1003, 'c2', 101, 'c4'),(1004, 'c2', 100, 'c4'),(1005, 'c2', 101, 'c4')
```
3. Create a Hive COS external table.
```
create table hive_cos_table(c1 int, c2 string, c3 int, c4 string) 
row format delimited fields terminated by ',' 
LINES TERMINATED BY '\n'
stored as textfile location 'cosn://{bucket_name}/{dir_name}';
```
For more information, see [Creating Databases Based on COS](https://intl.cloud.tencent.com/document/product/1026/31151).
4. Import the local data into COS.
```
insert into hive_cos_table select * from hive_local_table;
```
After successful write, you can see the file in the corresponding COS directory.
5. Create a COS external table in CDWPG.
```
CREATE READABLE EXTERNAL TABLE  snova_cos_table (c1 int, c2 varchar(32), c3 int, c4 varchar(32)) 
LOCATION('cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} secretKey=**** secretId=***')
FORMAT 'csv';
```
For more information, see [Importing and Exporting COS Data at High Speed with External Table](https://intl.cloud.tencent.com/document/product/1138/45032).
6. Create a local table in CDWPG and import data into it.
```
create table snova_local_table(c1 int, c2 text, c3 int, c4 text);
insert into snova_local_table select * from snova_cos_table;
```

