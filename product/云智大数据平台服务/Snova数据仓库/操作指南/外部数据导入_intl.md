## Importing CDB Data Using Kettle
Kettle is an open-source ETL tool written in pure Java language that runs on Windows, Linux and Unix and offers efficient and stable data extraction.
[Download address >>](http://kettle.pentaho.org/)
## Importing CDB Data Using data-loader
Data Loader is an easy command line tool that allows you to import full or incremental data from CDB into Snova. The tool is developed in Java and uses JDBC to connect the source and target databases. It can be run on Windows and Linux. Before use, you need to install the Java runtime environment and set the environment variable JAVA_HOME.
Basic structure:
![](https://main.qcloudimg.com/raw/4a69153ce9c4eb4a1c124f20e880f502.png)
Configuration file:
```
# Source database's JDBC driver. The corresponding driver is specified according to the database type
source.jdbc-driver:com.mysql.jdbc.Driver
# Source database's JDBC connection URL. See the following example for configuration; main configuration items include server address, port and database. In addition, useCursorFetch=true&defaultFetchSize=5000 means that the data is read in a streaming manner, which usually needs to be configured in order to avoid too high consumption of the memory by the tool
source.jdbc-url:jdbc:mysql://SourceCDB:4199/CDB?useCursorFetch=true&defaultFetchSize=5000
# Source database's username. Please ensure that the username has the permission to read the corresponding table
source.user:test
# Source database's password
source.password:abcd1234
# The SQL statement to extract the data from the source database. This supports the configuration of dynamic parameters (? indicates dynamic parameters). Parameters are passed in when the run.sh script is executed
source.sql:SELECT * FROM FlinkRawMetrics WHERE id>=? AND id<?
# If dynamic parameters are used in source.sql, you need to configure the parameter types. The following types are available:
# time - time type; number - number type; string - string type (default)
source.sql.args-type:time

# Target database's JDBC driver. For importing GP, set this to org.postgresql.Driver
target.jdbc-driver:org.postgresql.Driver
# Target database's JDBC connection URL. See the following example for configuration; main configuration items include server address, port and database. reWriteBatchedInserts=true means batch import is started, which can improve the import efficiency and thus usually needs to be set
target.jdbc-url:jdbc:postgresql://DevPG:50010/postgres?reWriteBatchedInserts=true
# Target database's username. Please ensure that the username has the permission to write the corresponding table
target.user:root
# Target database's password
target.password:abcd1234
# Table in the target database to which the data needs to be imported
target.table:FlinkRawMetrics
# Whether to clear the target table before importing, which usually needs to be set to true when importing full data
target.truncate-before-insert:true
# Whether to delete the data of this stage before importing. The dynamic parameters are used in the same way as in source.sql, which usually are set for incremental import to ensure that repeated incremental operations for the specified time period can get consistent results.
target.clear-sql-before-insert:DELETE FROM FlinkRawMetrics WHERE id>=? AND id<?
# Same usage as source.sql.args-type
target.clear-sql-before-insert.args-type:true
# Number of data entries imported in batches
target.batch-size:5000
```

### Preparations
1. Create a source table in TencentDB for MySQL using the following statement:
```
CREATE TABLE `EndpointAccessLog` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `time_` timestamp NULL DEFAULT NULL,
  `client_ip` varchar(16) DEFAULT NULL,
  `method` varchar(8) DEFAULT NULL,
  `uri` varchar(256) DEFAULT NULL,
  `protocol_version` varchar(16) DEFAULT NULL,
  `status_code` bigint(20) DEFAULT NULL,
  `app_id` bigint(20) DEFAULT NULL,
  `request_body_length` bigint(20) DEFAULT NULL,
  `response_body_length` bigint(20) DEFAULT NULL,
  `cost` bigint(20) DEFAULT NULL,
  `user_agent` varchar(256) DEFAULT NULL,
  `host` varchar(32) DEFAULT NULL,
  `date_` varchar(16) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `time_` (`time_`)
) ENGINE=InnoDB
```
An index is built on the time field for time-based incremental extraction.
2. Create a target table in Snova and create an index on the time field.

### Full Import
Full import is used to import all the data of the data source into the target database at one time and offline. It is only executed once and manually triggered by the OPS personnel.
1. Write a configuration file
```
source.jdbc-driver:com.mysql.jdbc.Driver
source.jdbc-url:jdbc:mysql://SourceCDB:4199/CDB?useCursorFetch=true&defaultFetchSize=5000
source.user:test
source.password:abcd1234
source.sql:SELECT * FROM EndpointAccessLog   
target.jdbc-driver:org.postgresql.Driver
target.jdbc-url:jdbc:postgresql://TargetGP:13634/postgres?reWriteBatchedInserts=true
target.user:gptestuser
target.password:gptestuser
target.table: EndpointAccessLog
target.truncate-before-insert:true
target.batch-size:5000
```
2. Insert data in the source table
```
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('1','2018-06-08 17:01:09','10.59.226.106','POST','/messages/1253358381/SngapmQQ/cttree/','HTTP/1.0','200','1253358381','144670','5','9','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('2','2018-06-08 17:01:09','10.59.226.106','POST','/messages/1253358381/SngapmQQ/cttree/','HTTP/1.0','200','1253358381','107876','5','21','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('3','2018-06-08 17:01:09','100.98.236.186','GET','/topics/1251001049/sngapmfutu/timelineheader','HTTP/1.0','404','0','0','17','19','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
```
3. Run a job
![](https://main.qcloudimg.com/raw/3eba392fc3b2c3326894dbd73691ef35.png)
View the data in the target GP and you can see that the data has been successfully imported:
![](https://main.qcloudimg.com/raw/049494e76841f43ec12094e5d74bbf63.png)

### Incremental Import
Incremental import is used to import the data newly added after the last job into the target database. Compared to full import, its trigger mode can be set to manual, but it is usually set to auto (such as every 5 minutes, hourly or daily) and released to the production environment for regular execution.
There are several ways to achieve incremental import. You need to set the corresponding scheduling policy according to the characteristics and requirements of the data source. This example uses the method of saving data with the current timestamp and timed import. Here, we use the hour for incremental import. We have imported the data of 17:00 on June 8, 2018 during the full import, and now we import the data of 18:00 on June 8, 2018.
1. Write a configuration file
```
source.jdbc-driver:com.mysql.jdbc.Driver
source.jdbc-url:jdbc:mysql://SourceCDB:4199/CDB?useCursorFetch=true&defaultFetchSize=5000
source.user:test
source.password:abcd1234
source.sql:SELECT * FROM EndpointAccessLog WHERE time_>=? AND time<?
source.sql.args-type:time
target.jdbc-driver:org.postgresql.Driver
target.jdbc-url:jdbc:postgresql://TargetGP:13634/postgres?reWriteBatchedInserts=true
target.user:gptestuser
target.password:gptestuser
target.table: EndpointAccessLog
target.clear-sql-before-insert:DELETE FROM EndpointAccessLog WHERE time_>=? AND time <?
target.clear-sql-before-insert.args-type:time
target.batch-size:5000
```
Here, `WHERE time_>=? AND time<?` is the incremental parameter and needs to be configured.
2. Insert new data in the source table
```
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('134240','2018-06-08 18:00:00','10.59.226.106','POST','/messages/1253358381/SngapmQQ/cttree/','HTTP/1.0','200','1253358381','109662','5','25','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('134241','2018-06-08 18:00:00','10.59.226.86','POST','/messages/1253358381/SngapmQQ/dfrate/','HTTP/1.0','200','1253358381','223329','5','21','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
insert into `EndpointAccessLog` (`id`, `time_`, `client_ip`, `method`, `uri`, `protocol_version`, `status_code`, `app_id`, `request_body_length`, `response_body_length`, `cost`, `user_agent`, `host`, `date_`) values('134242','2018-06-08 18:00:00','10.148.218.46','POST','/messages/1253358381/SngapmQQ/timelineio/','HTTP/1.0','200','1253358381','197122','5','28','CDP-SDK-JAVA/1.0','10_207_128_38','2018-06-08');
```
3. Run an incremental job
 ![](https://main.qcloudimg.com/raw/dd4556cccf8a6685b4a66917cdf27247.png)
After the completion, view the data in the target GP and you can see that in addition to the original data, the new data has been successfully imported.
![](https://main.qcloudimg.com/raw/28d8cd469b6c485b3d2067997771bede.png)

## Querying COS Data with COS_EXT
### Introduction
COS_EXT is an external data access plug-in for accessing COS files. By defining an external table using DDL, DML can be executed like a common data table to implement operations on COS data. Currently, it can be used:
- as an external table to read COS data;
- as an external table to export the results to COS;
- as an external table to perform simple analysis functions to analyze COS data.

### Steps
1. Define the cos_ext plug-in
  1. Note: The scope of the COS external table plug-in is a table.
  2. The creation command is as follows:
     ```
     CREATE EXTENSION IF NOT EXISTS cos_ext;
     ```
 3. The deletion command is as follows:
     ```
     DROP EXTENSION IF EXISTS cos_ext;
     ```
2. Define the COS external table; for syntax, see [Syntax Description](#codeintro)
3. Operate the data in the COS external table

### <a id="codeintro"></a>Syntax Explanations
1. Read-only input table definition
   ```
   CREATE [READABLE] EXTERNAL TABLE tablename
   ( columnname datatype [, ...] | LIKE othertable )
   LOCATION (cos_ext_params)
   FORMAT 'TEXT'
               [( [HEADER]
                  [DELIMITER [AS] 'delimiter' | 'OFF']
                  [NULL [AS] 'null string']
                  [ESCAPE [AS] 'escape' | 'OFF']
                  [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
                  [FILL MISSING FIELDS] )]
              | 'CSV'
               [( [HEADER]
                  [QUOTE [AS] 'quote']
                  [DELIMITER [AS] 'delimiter']
                  [NULL [AS] 'null string']
                  [FORCE NOT NULL column [, ...]]
                  [ESCAPE [AS] 'escape']
                  [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
                  [FILL MISSING FIELDS] )]
   [ ENCODING 'encoding' ]
   [ [LOG ERRORS [INTO error_table]] SEGMENT REJECT LIMIT count
          [ROWS | PERCENT] ]
   ```
2. Write-only output table definition
   ```
   CREATE WRITABLE EXTERNAL TABLE table_name
   ( column_name data_type [, ...] | LIKE other_table )
   LOCATION (cos_ext_params)
   FORMAT 'TEXT'
                  [( [DELIMITER [AS] 'delimiter']
                  [NULL [AS] 'null string']
                  [ESCAPE [AS] 'escape' | 'OFF'] )]
             | 'CSV'
                  [([QUOTE [AS] 'quote']
                  [DELIMITER [AS] 'delimiter']
                  [NULL [AS] 'null string']
                  [FORCE QUOTE column [, ...]] ]
                  [ESCAPE [AS] 'escape'] )]
   [ ENCODING 'encoding' ]
   [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
   ```
3. cos_ext_params description
   ```
   cos://cos_endpoint/bucket/prefix secretId=id secretKey=key compressiontype=[none|gzip] https=[true|false]
   ```

### Parameter Descriptions
| Parameters | Format | Required | Description |
| ------------ | ------------------------------------ | ---- | --------------------------------------- |
| URL          | cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX} | Yes   | See [URL Parameter Descriptions](#url)                |
| secretId     | Nil         | Yes   | Key ID used to access the API; see [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| secretKey     | Nil         | Yes   | Key ID used to access the API; see [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| https        | true &Iota; false       | No   | Whether to use HTTPS to access COS; true by default        |
| compressType | gzip            | No   | Whether to compress the COS files; blank by default for no compression            |

<a id="url"></a>
#### URL Parameter Descriptions
REGION: The region supported by COS. This has to be the same region as the instance. For available values, see [Regions and Access Domain Names](https://cloud.tencent.com/document/product/436/6224).
BUCKET: COS bucket name.
PREFIX: COS object name prefix which can be blank or include multiple slashes.
- In a read-only table, the prefix specifies the name prefix of the objects to be read.
  If the prefix is blank, all files in the bucket are read; if the prefix ends in a slash (/), all files in the folder and subfolders are matched; otherwise, all files in the folder and subfolders matching the prefix are read. 
  For example, COS objects include:
  read-bucket/simple/a.csv
  read-bucket/simple/b.csv
  read-bucket/simple/dir/c.csv
  read-bucket/simple_prefix/d.csv
 - If the prefix is specified as simple, all files are read, including the simple_prefix object list that matches the directory name prefix:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/dir/c.csv
    read-bucket/simple_prefix/d.csv
 - If the prefix is specified as simple/, all the files containing simple/ are read, including:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/dir/c.csv
- In a write-only table, the prefix specifies the output file prefix.
  If no prefix is specified, the files are written to the bucket; if the prefix ends in a slash (/), the files are written to the directory specified by the prefix; otherwise, the given prefix is used as the file prefix. 
  For example, the files that need to be created include: 
  a.csv, b.csv, c.csv
 - If the prefix is specified as simple/, the generated objects are:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/b.csv
 - If the prefix is specified as simple_, the generated objects are:
    read-bucket/simple_a.csv
    read-bucket/simple_b.csv
    read-bucket/simple_b.csv

### Usage Examples
1. Importing COS data
   1. Define the COS extension:  
      ```
      CREATE EXTENSION IF NOT EXISTS cos_ext; 
      ```
   2. Define the read-only COS external table and local table
       Local table:
     ```
     CREATE TABLE cos_local_tbl (c1 int, c2 text, c3 int)
     DISTRIBUTED BY (c1);
     ```
     COS external table: Specify to read all files under simple-bucket in Guangzhou.
     ```
     CREATE READABLE EXTERNAL TABLE cos_tbl (c1 int, c2 text, c3 int)
     LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/from_cos/ secretKey=xxx secretId=xxx')
     FORMAT 'csv';
     ```
   3. Prepare local table data
      Upload the file to the from_cos directory in simple-bucket with the following content:
      ```
      1,simple line 1,1
      2,simple line 1,1
      3,simple line 1,1
      4,simple line 1,1
      5,simple line 1,1
      6,simple line 2,1
      7,simple line 2,1
      8,simple line 2,1
      9,simple line 2,1
      ```
    4. Import COS data
    ```
   INSERT INTO cos_local_tbl SELECT * FROM cos_tbl;
    ```
   5. View the result and compare the data for consistency
      ```
      SELECT count(1) FROM cos_local_tbl;
      SELECT count(1) FROM cos_tbl;
      ```
2. Exporting data to COS
 1. Define COS extension
```
CREATE EXTENSION IF NOT EXISTS cos_ext;
```
 2. Define the write-only COS external able
Local table:
```
CREATE TABLE cos_local_tbl (c1 int, c2 text, c3 int)
DISTRIBUTED BY (c1);
```
COS external table: Specify to read all files under simple-bucket in Guangzhou.
```
CREATE WRITABLE EXTERNAL TABLE cos_tbl_wr (c1 int, c2 text, c3 int)
LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/to-cos/ secretKey=xxx secretId=xxx')
FORMAT 'csv';
```
 3. Construct test data
```
insert into cos_local_tbl values
(1, 'simple line 1' , 1),
(2, 'simple line 2', 2), 
(3, 'simple line 3', 3) ,
(4, 'simple line 4', 4) , 
(5, 'simple line 5', 5) ,
(6, 'simple line 6', 6) , 
(7, 'simple line 7', 7) , 
(8, 'simple line 8', 8) , 
(9, 'simple line 9', 9);
```
 4. Export data to COS
```
INSERT INTO cos_tbl_wr SELECT * FROM cos_local_tbl;
```
 5. View the result
![](https://main.qcloudimg.com/raw/28d8cd469b6c485b3d2067997771bede.png)

3. Simple COS data analysis
>**Note:**
Queries and analyses using COS external tables are not optimized, so it is recommended to import data to local tables before running complex queries. 

   1. Define COS extension
   ```
   CREATE EXTENSION IF NOT EXISTS cos_ext;
   ```
  2. Prepare data
 Upload the file to the for-dml directory in simple-bucket with the following content:
   ```
   1,simple line 1,1
   2,simple line 1,1
   3,simple line 1,1
   4,simple line 1,1
   5,simple line 1,1
   6,simple line 2,1
   7,simple line 2,1
   8,simple line 2,1
   9,simple line 2,1
   ```
   3. Define the read-only COS external table
   ```
   CREATE READABLE EXTERNAL TABLE cos_tbl_dml (c1 int, c2 text, c3 int)
   LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/for-dml/ secretKey=xxx secretId=xxx')
   FORMAT ‘csv’;
   ```
 4. Analyze the data in the COS external table
   ```
   SELECT c2, sum(c1) FROM cos_tbl GROUP BY c2;
   ```
