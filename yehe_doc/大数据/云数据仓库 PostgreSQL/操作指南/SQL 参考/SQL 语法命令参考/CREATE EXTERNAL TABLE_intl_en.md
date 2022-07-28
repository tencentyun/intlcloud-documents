It defines a new external table. Currently, CDW only supports Tencent Cloud COS external tables but not gpfdist, file, S3, HDFS, and HTTP external tables.

## Synopsis
```sql
CREATE [READABLE] EXTERNAL TABLE table_name     
    ( column_name data_type [, ...] | LIKE other_table )
     LOCATION 
('cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} secretKey=xxx secretId=xxx '
           [, ...])| ('cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX} secretKey=xxx secretId=xxx ')
     [ON MASTER]
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
          | 'AVRO' 
          | 'PARQUET'
          | 'CUSTOM' (Formatter=<formatter_specifications>)
    [ ENCODING 'encoding' ]
      [ [LOG ERRORS] SEGMENT REJECT LIMIT count
      [ROWS | PERCENT] ]
 
 
CREATE WRITABLE EXTERNAL TABLE table_name
    ( column_name data_type [, ...] | LIKE other_table )
     LOCATION('cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} secretKey=xxx secretId=xxx '
           [, ...])| ('cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX} secretKey=xxx secretId=xxx ' [, ...])
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
           | 'AVRO' 
           | 'PARQUET'
 
           | 'CUSTOM' (Formatter=<formatter specifications>)
    [ ENCODING 'write_encoding' ]
    [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
 
```

## Description
For information about external tables, see "Loading and Unloading Data" in the Database Administrator Guide.

`CREATE EXTERNAL TABLE` or `CREATE EXTERNAL WEB TABLE` creates a new readable external table definition in the database. Readable external tables are typically used for fast, parallel data loading. Once an external table is defined, you can query its data directly (and in parallel) using SQL commands. For example, you can select, join, or sort external table data. You can also create views for external tables. DML operations (`UPDATE`, `INSERT`, `DELETE`, or `TRUNCATE`) are not allowed on readable external tables, and you cannot create indexes on readable external tables.

`CREATE WRITABLE EXTERNAL TABLE` or `CREATE WRITABLE EXTERNAL WEB TABLE` creates a new writable external table definition in the database. Writable external tables are typically used for unloading data from the database into a set of files or named pipes. Writable external web tables can also be used to output data to an executable program. Once a writable external table is defined, data can be selected from database tables and inserted into the writable external table. Writable external tables only allow `INSERT` operations – `SELECT`, `UPDATE`, `DELETE` or `TRUNCATE` are not allowed.

The main difference between regular external tables and external web tables is their data sources. Regular readable external tables access static flat files, whereas external web tables access dynamic data sources – either on a web server or by executing OS commands or scripts.

The `FORMAT` clause describes the format of an external table file. Valid formats include delimited text (TEXT) and comma separated values (CSV) formats, and formatting options are similar to those available with the PostgreSQL **`COPY`** command. If the data in the file does not use the default column delimiter, escape character, null string and so on, you must specify the additional formatting options so that the data in the external file is read correctly by the database. For information about using a custom format, see "Loading and Unloading Data" in the Database Administrator Guide.

Before creating an external table that writes to or reads from a COS store, the database must be configured to support the protocol. COS external tables can use files in CSV or text format. Writable COS external tables only support `INSERT`. For more information, see **COS Protocol Configuration**.

## Parameters
READABLE | WRITABLE
Specifies the type of external table, readable being the default. Readable external tables are used for loading data into the database. Writable external tables are used for unloading data.

table_name
The name of the new external table.

column_name
The name of a column to create in the external table definition. Unlike regular tables, external tables do not have column constraints or default values, so do not specify those.

LIKE other_table
The `LIKE` clause specifies a table from which the new external table automatically copies all column names, data types and distribution policy. If the original table specifies any column constraints or default column values, those will not be copied over to the new external table definition.

data_type
The data type of the column.

LOCATION ('protocol://host[:port]/path/file' [, ...])
For readable external tables, specifies the URI of the external data source(s) to be used to populate the external table or web table. Regular readable external tables allow the gpfdist or file protocols. External web tables allow the HTTP protocol. If port is omitted, port 8080 is assumed for HTTP and gpfdist protocols, and port 9000 for the gphdfs protocol. If using the gpfdist protocol, the path is relative to the directory from which gpfdist is serving files (the directory specified when you started the gpfdist program). Also, gpfdist can use wildcards or other C-style pattern matching (for example, a whitespace character is [[:space:]]) to denote multiple files in a directory. For example:

```sql
'gpfdist://filehost:8081/*'
'gpfdist://masterhost/my_load_file'
'file://seghost1/dbfast1/external/myfile.txt'
'http://intranet.example.com/finance/expenses.csv'
'cos://{BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} secretKey=xxx secretId=xxx'
```
 
For writable external tables, specifies the URI location of the COS protocol that will collect data output from the segments and write it to one or more named files. 

With the option `#transform=trans_name`, you can specify a transform to apply when loading or extracting data. The `trans_name` is the name of the transform in the YAML configuration file you specify when you run the gpfdist utility. When you create an external table with the **COS** protocol, only TEXT and CSV formats are supported. These files can be in gzip compressed format. The **COS** protocol recognizes the gzip format and decompresses files. Only the gzip compression format is supported.

EXECUTE 'command' [ON ...]
Allowed for readable external web tables or writable external tables only. For readable external web tables, specifies the OS command to be executed by the segment instances. The command can be a single OS command or a script. The `ON` clause is used to specify which segment instances will execute the given command.

FORMAT 'TEXT | CSV | AVRO | PARQUET' (options)
Specifies the data format of the external or web table, which can be text (TEXT) or comma separated values (CSV) format.
The AVRO and PARQUET formats are supported only when you specify the gphdfs protocol.

FORMAT 'CUSTOM' (formatter=formatter_specification)
Specifies a custom data format. The `formatter_specification` specifies the function to use to format the data, followed by comma-separated parameters to the formatter function. The length of the formatter specification, the string including `Formatter=`, can be up to approximately 50K bytes.

For general information about using a custom format, see "Loading and Unloading Data" in the Database Administrator Guide.

DELIMITER
Specifies a single ASCII character that separates columns within each row (line) of data. The default is a tab character in TEXT mode, a comma in CSV mode. In TEXT mode for readable external tables, the delimiter can be set to OFF for special use cases in which unstructured data is loaded into a single-column table.

NULL
Specifies the string that represents a NULL value. The default is \N (backslash-N) in TEXT mode, and an empty value with no quotations in CSV mode. You might prefer an empty string even in TEXT mode for cases where you do not want to distinguish NULL values from empty strings. When using external and web tables, any data item that matches this string will be considered a NULL value.

As an example for the text format, this `FORMAT` clause can be used to specify that the string of two single quotes ('') is a NULL value.

```sql
FORMAT 'text' (delimiter ',' null '\'\'\'\'' )
```

ESCAPE
Specifies the single character that is used for C escape sequences (such as \n,\t,\100, and so on) and for escaping data characters that might otherwise be taken as row or column delimiters. Make sure to choose an escape character that is not used anywhere in your actual column data. The default escape character is a \ (backslash) for text-formatted files and a " (double quote) for CSV-formatted files, however it is possible to specify another character to represent an escape. It is also possible to disable escaping in text-formatted files by specifying the value 'OFF' as the escape value. This is very useful for data such as text-formatted web log data that has many embedded backslashes that are not intended to be escapes.

NEWLINE
Specifies the newline used in your data files – LF (Line feed, 0x0A), CR (Carriage return, 0x0D), or CRLF (Carriage return plus line feed, 0x0D 0x0A). If not specified, a database segment will detect the newline type by looking at the first row of data it receives and using the first newline type encountered.

HEADER
For readable external tables, specifies that the first line in the data file(s) is a header row (contains the names of the table columns) and should not be included as data for the table. If using multiple data source files, all files must have a header row.

For the s3 protocol, the column names in the header row cannot contain a newline character (\n) or a carriage return (\r).

QUOTE
Specifies the quotation character for CSV mode. The default is double-quote (").

FORCE NOT NULL 
In CSV mode, processes each specified column as though it were quoted and hence not a NULL value. For the default null string in CSV mode (nothing between two delimiters), this causes missing values to be evaluated as zero-length strings.

FORCE QUOTE
In CSV mode for writable external tables, forces quoting to be used for all non-NULL values in each specified column. NULL output is never quoted.

FILL MISSING FIELDS
In both TEXT and CSV mode for readable external tables, specifying `FILL MISSING FIELDS` will set missing trailing field values to NULL (instead of reporting an error) when a row of data has missing data fields at the end of a line or row. Blank rows, fields with a `NOT NULL` constraint, and trailing delimiters on a line will still report an error.

ENCODING 'encoding'
Character set encoding to use for the external table. Specify a string constant (such as 'SQL_ASCII'), an integer encoding number, or `DEFAULT` to use the default client encoding. 

LOG ERRORS
This is an optional clause that can precede a `SEGMENT REJECT LIMIT` clause to log information about rows with formatting errors. The error log data is stored internally, and is accessed with the database built-in SQL function `gp_read_error_log()`.

SEGMENT REJECT LIMIT count [ROWS | PERCENT]
Runs a `COPY FROM` operation in single row error isolation mode. If the input rows have format errors they will be discarded provided that the reject limit count is not reached on any segment instance during the load operation. The reject limit count can be specified as number of rows (the default) or percentage of total rows (1-100). If `PERCENT` is used, each segment starts calculating the bad row percentage only after the number of rows specified by the parameter `gp_reject_percent_threshold` has been processed. The default for `gp_reject_percent_threshold` is 300 rows. Constraint errors such as violation of a `NOT NULL`, `CHECK`, or `UNIQUE` constraint will still be handled in "all-or-nothing" input mode. If the limit is not reached, all good rows will be loaded and any error rows discarded.

Note: When reading an external table, the database limits the initial number of rows that can contain formatting errors if the `SEGMENT REJECT LIMIT` is not triggered first or is not specified. If the first 1000 rows are rejected, the `COPY` operation is stopped and rolled back.

The limit for the number of initial rejected rows can be changed with the database server configuration parameter `gp_initial_bad_row_limit`. 

DISTRIBUTED BY (column, [ ... ] )
DISTRIBUTED RANDOMLY
Used to declare the database distribution policy for a writable external table. By default, writable external tables are distributed randomly. If the source table you are exporting data from has a hash distribution policy, defining the same distribution key column(s) for the writable external table will improve unload performance by eliminating the need to move rows over the interconnect. When you issue an unload command such as `INSERT INTO wex_table SELECT * FROM source_table`, the rows that are unloaded can be sent directly from the segments to the output location if the two tables have the same hash distribution policy.

## Examples
Create a readable external table named `cos_tbl` using the COS protocol and designate to read all CSV files in the `simple-bucket` in Guangzhou:
```sql
CREATE READABLE EXTERNAL TABLE cos_tbl (c1 int, c2 text, c3 int)
LOCATION('cos://cos.ap-guangzhou.myqcloud.com/simple-bucket/from_cos/ secretKey=xxx secretId=xxx')
FORMAT 'csv';
```

## Notes
When you specify the `LOG ERRORS` clause, the database captures errors that occur while reading the external table data. You can view and manage the captured error log data.
- Use the built-in SQL function `gp_read_error_log('table_name')`, which requires `SELECT` privilege on the `table_name`. This example displays the error log information of the data loaded into the table `ext_expenses` using the `COPY` command:
```sql
SELECT * from gp_read_error_log('ext_expenses');
```
The function returns `FALSE` if the table does not exist.
- If error log data exists for a specified table, new data is appended to existing error log data. The error log data is not replicated to mirror segments.
- Use the built-in SQL function `gp_truncate_error_log('table_name')` to delete the error log data for `table_name`, which requires the table owner privilege. This example deletes the error log information captured when data is moved into the table `ext_expenses` :
```sql
SELECT gp_truncate_error_log('ext_expenses'); 
```
The function returns `FALSE` if the table does not exist.

You can use the `\*` wildcard character to delete error log information for existing tables in the current database. Specify the string *.* to delete all database error log information, including error log information that was not deleted due to previous database issues. If \* is specified, database owner privilege is required. If *.* is specified, operating system superuser privilege is required.

## COS Protocol Restrictions
- Only URLs in the COS path style are supported.
```sql
--COS V4: 
cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX}
--COS V5: 
cos:// {BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX}
```
- Only one URL is supported in the `LOCATION` clause of the `CREATE EXTERNAL TABLE` command.
- If the `NEWLINE` parameter is not specified in the `CREATE EXTERNAL TABLE` command, the newline character must be the same in all data files with the specified prefix. Read operations on files may fail if the newline characters differ in some data files with the same prefix.
- Writable COS external tables support only `INSERT` but not `UPDATE`, `DELETE`, and `TRUNCATE`.
- In the parallel processing of segment instances by the database, files in the COS location of the read-only COS table should have similar sizes, and the number of files should be the same as the number of segments.

## Notes on COS URL
For the COS protocol, you can specify the file location and optional configuration file location in the `LOCATION` clause of the `CREATE EXTERNAL TABLE` command. The syntax is as follows:
```sql
'cos://cos.{REGION}.myqcloud.com/{BUCKET}/{PREFIX} secretKey=xxx secretId=xxx'
'cos://{BUCKET}-{APPID}.cos.{REGION}.myqcloud.com/{PREFIX} secretKey=xxx secretId=xxx'
```
You can specify the COS protocol to access data in Tencent Cloud COS. For the COS protocol, the `LOCATION` clause specifies the COS endpoint and bucket name where data files are uploaded for the table.
- REGION: Region supported by COS, which needs to be the same region as the instance. For valid values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- BUCKET: COS bucket name.
- PREFIX: COS object name prefix, which can be empty and include multiple "/".

In the scenario of defining a read-only table, the `prefix` specifies the name prefix of objects to be read. If `prefix` is empty, all files in the bucket will be read; if it ends with "/", all files in the folder and subfolders will be matched; otherwise, all files in the folder and subfolders matched by `prefix` will be read. For example, COS objects include:
```
read-bucket/simple/a.csv
read-bucket/simple/b.csv
read-bucket/simple/dir/c.csv
read-bucket/simple_prefix/d.csv
```
If `prefix` is specified as `simple`, all files will be read, including `simple_prefix` with the matching directory name prefix. The following is the list of objects:
```
read-bucket/simple/a.csv
read-bucket/simple/b.csv
read-bucket/simple/dir/c.csv
read-bucket/simple_prefix/d.csv
```
If `prefix` is specified as `simple/`, all files including `simple/` will be read, including:
```
read-bucket/simple/a.csv
read-bucket/simple/b.csv
read-bucket/simple/dir/c.csv
```

In the write-only table scenario, the `prefix` specifies the output file prefix. If no `prefix` is specified, files will be written to the bucket. If `prefix` ends with "/", files will be written to the directory specified by `prefix`; otherwise, files will be prefixed with the given `prefix`. For example, if the files that need to be created include `a.csv`, `b.csv`, and `c.csv`, then:

- If `prefix` is specified as `simple/`, the following objects will be generated:
```
read-bucket/simple/a.csv
read-bucket/simple/b.csv
read-bucket/simple/b.csv
```
- If `prefix` is specified as `simple\_`, the following objects will be generated:
```
read-bucket/simple_a.csv
read-bucket/simple_b.csv
read-bucket/simple_b.csv
```

`secretKey` and `secretId` are your own key pair in Tencent Cloud.

**Note**: When uploading or downloading COS files, the database may require up to threadnum * chunksize memory on each segment host. When you configure the overall database memory, take into account this COS protocol memory requirement and increase the value of **gp_vmem_protect_limit** as needed.

## Compatibility
`CREATE EXTERNAL TABLE` is a database extension. The SQL standard makes no provisions for external tables.

## See Also
CREATE TABLE AS, CREATE TABLE, COPY, SELECT INTO, INSERT
