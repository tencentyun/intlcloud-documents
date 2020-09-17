ClickHouse allows you to import data stored in COS to tables in two methods:
- Table engine: you can create an `Engine=S3` external table to import data.
- Table function: you can use a built-in function to import data.

Before using the two methods above, you need to see the table below to set COS access permission:

|EMR |	ClickHouse	|COS Access Permission	|Table Engine|
|---------|---------|---------|----|
|1.0.0	|19.16.12.49	|Public read/write|	S3|
|1.1.0	|20.3.10.75| Public read/write, authenticated read/write (by secretId and secretKey)	|S3|
|1.2.0+	|20.7.2.30	| Public read/write, authenticated read/write (by secretId and secretKey)	|S3, COSN|

## Using Table Engine

You can create an external table and a destination table whose engine is `S3` and use the `INSERT INTO` statement to insert data in batches.
```
CREATE TABLE testdb.costb (
    column1 UInt32, 
    column2 String,
    column3 String
) ENGINE=S3 ('http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 'CSV');
Or
CREATE TABLE testdb.costb (
    column1 UInt32, 
    column2 String,
    column3 String
) ENGINE=S3('http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 'secretId', 'secretKey', 'CSV');
Or
CREATE TABLE testdb.costb (
    column1 UInt32, 
    column2 String,
    column3 String
) ENGINE=COSN('http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 'secretId', 'secretKey', 'CSV');

CREATE TABLE testdb.chtb (
    column1 UInt32, 
    column2 String, 
    column3 String
) ENGINE=MergeTree() ORDER BY(column1);

INSERT INTO testdb.chtb SELECT * FROM testdb.costb;
```
If you are using version EMR 1.2.0 or later (ClickHouse 20.7.2.30+), you can change the table engine S3 to COSN, and get the same result.

## Using Table Function

When creating a table, you can use the `s3` built-in function to directly import data into it.
```
CREATE TABLE testdb.chtb
ENGINE=MergeTree() 
ORDER BY(column1) 
AS SELECT * FROM s3(
  'http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 
  'CSV', 'column1 UInt32, column2 String, column3 String');
Or
CREATE TABLE testdb.chtb
    ENGINE=MergeTree() 
    ORDER BY(column1) 
    AS SELECT * FROM s3(
      'http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 'secretId', 'secretKey',
      'CSV', 'column1 UInt32, column2 String, column3 String');
```

## References

- [CREATE Queries](https://clickhouse.tech/docs/en/query_language/create/)
- [Support S3 as the persistent storage](https://github.com/ClickHouse/ClickHouse/issues/1394)
