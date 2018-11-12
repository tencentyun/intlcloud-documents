## Overview
COS_EXT is an external data access plug-in for accessing COS files. By defining an external table using DDL, DML can be executed like a common data table to implement operations on COS data. Currently, it can be used:
- as an external table to read COS data;
- as an external table to export the results to COS;
- as an external table to perform simple analysis functions to analyze COS data.

## Steps
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

## <a id="codeintro"></a>Syntax Description
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

## Parameter Descriptions
| Parameters | Format | Required | Description |
| ------------ | ------------------------------------ | ---- | --------------------------------------- |
| URL          | COS V4： cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX}<br>COS V5： cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} | Yes   | See [URL Parameter Descriptions](#url)                |
| secretId     | Nil         | Yes   | Key ID used to access the API; see [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| secretKey     | Nil         | Yes   | Key ID used to access the API; see [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| https        | ture\false       | No   | Whether to use HTTPS to access COS; true by default        |
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

## Usage Examples
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
