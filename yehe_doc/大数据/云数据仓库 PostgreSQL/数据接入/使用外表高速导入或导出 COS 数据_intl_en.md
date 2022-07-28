## Querying COS Data with COS_EXT
COS_EXT is an external data access extension for accessing COS files. By defining an external table through DDL, you can run DML in the external table as a normal data table to manipulate COS data. The following are supported currently:
- Read COS data as an external table.
- Export results to COS as an external table.
- Perform simple analysis of COS data as an external table.

### Notes
1. Only files in text formats such as CSV and GZIP compressed format files are supported.
2. Only COS data in the same region can be read. For example, a cluster in Guangzhou Zone 4 can only read COS data in the Guangzhou region.
3. Only your own COS data can be read by your cluster.
4. Write-only external tables can only be used for the `INSERT` statement but not `UPDATE`, `DELETE`, and `SELECT` statements.
5. Deleting an external table will not delete the corresponding data in COS.

### Directions
1. Define the COS_EXT extension.
>!The scope of the COS external table extension is the database.
>
 - The creation command is as follows:
```
CREATE EXTENSION IF NOT EXISTS cos_ext SCHEMA public;
```
 - The deletion command is as follows:
```
DROP EXTENSION IF EXISTS cos_ext;
```
2. Define the COS external table. For syntax, see [Syntax description](#codeintro).
3. Manipulate data in the COS external table.

[](id:codeintro)
### Syntax description
- Definite the read-only input table
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
- Define the write-only output table
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
			[FORCE QUOTE column [, ...] ]
			[ESCAPE [AS] 'escape'] )]
   [ ENCODING 'encoding' ]
   [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
```
3. `cos_ext_params` description
```
cos://cos_endpoint/bucket/prefix secretId=id secretKey=key compressType=[none|gzip] https=[true|false]
```


### Parameter description

| Parameter         | Format              | Required | Description                            |
| ------------ | ------------------------------------ | ---- | --------------------------------------- |
| URL          | <li/>COS V4: `cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX}`<li/>COS V5: `cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX}`  | Yes   | See [URL parameter description](#url)                |
| secretId     | None         | Yes   | Secret ID used for API access. See [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| secretKey     | None         | Yes   | Secret key used for API access. See [API Key Management](https://console.cloud.tencent.com/cam/capi) |
| HTTPS        | true &Iota; false       | No   | Whether to use HTTPS to access COS. Default value: true        |
| compressType | gzip            | No   | Whether to compress COS files. Default value: empty (not to compress)            |

[](id:url)
#### URL parameter description
- REGION: Region supported by COS, which needs to be the same region as the instance. For valid values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- BUCKET: COS bucket name, which can be seen in [COS Bucket List](https://console.cloud.tencent.com/cos5/bucket). **The name here does not contain the `APPID`**. If you see the bucket name `test-123123123` in the list, just enter "test".
- PREFIX: COS object name prefix, which can be empty and include multiple "/".
 - In a read-only table scenario, `prefix` specifies the name prefix of the object to be read.
If `prefix` is empty, all files in the bucket will be read; if it ends with "/", all files in the folder and subfolders will be matched; otherwise, all files in the folder and subfolders matched by `prefix` will be read. For example, COS objects include `read-bucket/simple/a.csv`, `read-bucket/simple/b.csv`, `read-bucket/simple/dir/c.csv`, and `read-bucket/simple_prefix/d.csv`.
   - If `prefix` is specified as `simple`, all files will be read, including `simple_prefix` with the matching directory name prefix. The following is the list of objects:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/dir/c.csv
    read-bucket/simple_prefix/d.csv
   - If `prefix` is specified as `simple/`, all files including `simple/` will be read, including:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/dir/c.csv
 - In a write-only table scenario, `prefix` specifies the output file prefix.
If no `prefix` is specified, files will be written to the bucket. If `prefix` ends with "/", files will be written to the directory specified by `prefix`; otherwise, files will be prefixed with the given `prefix`. For example, if the files that need to be created include `a.csv`, `b.csv`, and `c.csv`, then:
   - If `prefix` is specified as `simple/`, the following objects will be generated:
    read-bucket/simple/a.csv
    read-bucket/simple/b.csv
    read-bucket/simple/b.csv
   - If `prefix` is specified as `simple\_`, the following objects will be generated:
    read-bucket/simple_a.csv
    read-bucket/simple_b.csv
    read-bucket/simple_b.csv

## Use Cases
### Importing COS data
1. Define the COS extension.  
```
CREATE EXTENSION IF NOT EXISTS cos_ext SCHEMA public; 
```
2. Define a COS read-only external table and a local table.
Local table:
```
CREATE TABLE cos_local_tbl (c1 int, c2 text, c3 int)
DISTRIBUTED BY (c1);
```
COS external table: Specifies to read all files in `simple-bucket` in Guangzhou.
```
CREATE READABLE EXTERNAL TABLE cos_tbl (c1 int, c2 text, c3 int)
LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/from_cos/ secretKey=xxx secretId=xxx')
FORMAT 'csv';
```
3. Prepare local table data.
Upload the file to the `from_cos` directory in `simple-bucket` with the following content:
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
>!The imported data does not contain field rows of the table header.
4. Import COS data.
```
INSERT INTO cos_local_tbl SELECT * FROM cos_tbl;
```
5. Check the result to see whether the data is consistent.
```
SELECT count(1) FROM cos_local_tbl;
SELECT count(1) FROM cos_tbl;
```

### Exporting data to COS
1. Define the COS extension.
```
CREATE EXTENSION IF NOT EXISTS cos_ext SCHEMA public;
```
2. Define a COS write-only external table.
Local table:
```
CREATE TABLE cos_local_tbl (c1 int, c2 text, c3 int)
DISTRIBUTED BY (c1);
```
COS external table: Specifies to write all files in `simple-bucket` in Guangzhou.
```
CREATE WRITABLE EXTERNAL TABLE cos_tbl_wr (c1 int, c2 text, c3 int)
LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/to-cos/ secretKey=xxx secretId=xxx')
FORMAT 'csv';
```
3. Construct the test data.
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
4. Export the data to COS.
```
INSERT INTO cos_tbl_wr SELECT * FROM cos_local_tbl;
```
5. Check the result.
![](https://qcloudimg.tencent-cloud.cn/raw/e6a21a8682ef72d8a31805c9331577e6.png)


### Simple analysis of COS data
>!When using COS external tables for query analysis without query optimization, we recommend you first import the data locally for complex queries. 
>
1. Define the COS extension.
```
CREATE EXTENSION IF NOT EXISTS cos_ext SCHEMA public;
```
2. Prepare the data.
Upload the file to the `for-dml` directory in `simple-bucket` with the following content:
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
3. Define a COS read-only external table.
```
CREATE READABLE EXTERNAL TABLE cos_tbl_dml (c1 int, c2 text, c3 int)
LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/for-dml/ secretKey=xxx secretId=xxx')
FORMAT 'csv';
```
4. Analyze the data in the COS external table.
```
SELECT c2, sum(c1) FROM cos_tbl GROUP BY c2;
```
