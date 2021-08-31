## Data Import
### Directly writing data with INSERT
You can use `INSERT` statements to write data into TDSQL-A for PostgreSQL tables. After using the psql client to connect to the database, you can run `INSERT INTO … VALUES` or `INSERT INTO…SELECT` to write data. TDSQL-A for PostgreSQL also allows you to connect to the database through APIs for JDBC, ODBC, Python, CAPI, ADO.NET, etc. and run `INSERT` statements to write data.

### Importing data with COPY FROM
In addition to `INSERT`, TDSQL-A for PostgreSQL also allows you to use the `COPY` command to copy data between files and tables in the following syntax:
```
COPY table_name [ ( column_name [, ...] ) ]
  FROM { 'filename' | PROGRAM 'command' | STDIN }
  [ [ WITH ] ( option [, ...] ) ]
COPY { table_name [ ( column_name [, ...] ) ] | ( query ) }
  TO { 'filename' | PROGRAM 'command' | STDOUT }
  [ [ WITH ] ( option [, ...] ) ]
```
Here, `option` can be one of the following options:
```
FORMAT format_name
OIDS [ boolean ]
FREEZE [ boolean ]
DELIMITER 'delimiter_character'
NULL 'null_string'
HEADER [ boolean ]
QUOTE 'quote_character'
ESCAPE 'escape_character'
FORCE_QUOTE { ( column_name [, ...] ) | * }
FORCE_NOT_NULL ( column_name [, ...] )
FORCE_NULL ( column_name [, ...] )
ENCODING 'encoding_name'
```
A `COPY` command with a filename indicates that the TDSQL-A for PostgreSQL server will directly read data from a file or write data to a file. The file must be accessible to users who run the TDSQL-A for PostgreSQL server, and it should be named from the perspective of the server.
After `PROGRAM` is specified, the server will run the given command and read data from the program's standard output (`STDOUT`) or write data to the program's standard input (`STDIN`). The program must be specified from the perspective of the server and be executable by the `tdapg` user.
If `STDIN` or `STDOUT` is specified, the data will be transferred through the connection between the client and the server.
In addition, `\COPY FROM/TO` can be used to copy a local file to a table or copy data in a table to a local file.

#### Loading multiple data sources
- STDIN:
```
postgres=# COPY tdapg (id, mc) FROM stdin;
Enter data to be copied followed by a newline.
End with a backslash and a period on a line by itself.
>> 1  tdapg
>> 2  \N
>> 3  pgxc
>> \.
postgres=# select * from tdapg;
 id | mc  
----+-------
 1 | tdapg
 2 | 
 3 | pgxc
(3 rows)
```
- SFTP data source:
Environment preparations: install the SFTP service and upload the data file to the SFTP server.
```
postgres=# COPY copy_hdfs FROM PROGRAM 'hadoop fs -cat hdfs://10.183.208.190:9000/lineitem' DELIMITER '|';
COPY 797000000
```
- HTTP data source:
Environment preparations: install the httpd service and upload the data file to the HTTP server.
```
postgres =# \COPY copy_http FROM PROGRAM 'curl -s http://10.183.208.191:8081/lineitem.csv' WITH csv DELIMITER ',';
COPY 797000000
```
- HDFS data source:
Environment preparations: install the Hadoop service and upload the data file to the Hadoop server.
```
postgres =# COPY copy_hdfs FROM PROGRAM 'hadoop fs -cat hdfs://10.183.208.190:9000/lineitem' DELIMITER '|';
COPY 797000000
```

#### Loading multiple data formats
`COPY` supports importing data from multiple data file formats such as CSV, TXT, GZIP, and SNAPPY.

- Import a CSV file:
```
postgres =# \COPY copy_csv FROM '/data12/copy_test_data/lineitem.csv' WITH csv DELIMITER ',';
COPY 797000000
```
- Import a TXT file:
```
postgres =# \COPY copy_csv FROM '/data12/copy_test_data/lineitem.txt' WITH (FORMAT 'text', DELIMITER '|');
COPY 797000000
```
- Import a SNAPPY file:
```
postgres=# \COPY copy_snappy FROM PROGRAM 'snzip -dc /data12/copy_test_data/lineitem.snappy' DELIMITER '|';
COPY 797000000
```
- Import a GZIP file:
```
postgrs=# \COPY copy_gzip FROM PROGRAM 'tar -zxvf /data12/copy_test_data/lineitem.tar.gz | xargs cat' DELIMITER '|';
COPY 797000000
```
- Import a LZO file:
```
postgres=# \COPY copy_lzop FROM PROGRAM 'lzop -cd /data12/copy_test_data/lineitem.lzo | more' DELIMITER '|'; 
COPY 797000000
```

## Data Export
Use `COPY TO` or `\COPY TO` to copy table data to a file:
```
COPY copyperf_txt TO '/data12/copy_test_data/cpto/cpto1.dat' WITH(FORMAT csv, DELIMITER ',');
```

Import table data to multiple data files:
```
COPY copyperf_txt TO PROGRAM 'cd /data12/copy_test_data/cpto && split -l 39850000 -d -a 4 && ls | grep ^x | xargs -n1 -i{} mv {} perfcopyto_{}.csv' WITH csv DELIMITER ',';
```
