ClickHouse allows you to import data stored in COS to tables in two methods:
- Table engine: you can create an `Engine=S3` external table to import data.
- Table function: you can use a built-in function to import data.

Before using the two methods above, you need to set COS to publicly readable. Currently, read/write of the authentication method (through `secretId` and `secretKey`) is not supported.

## Using Table Engine

You can create an external table and a destination table whose engine is `S3` and use the `INSERT INTO` statement to insert data in batches.
```
CREATE TABLE testdb.costb (
    column1 UInt32, 
    column2 String,
    column3 String
) ENGINE=S3 ('http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 'CSV');

CREATE TABLE testdb.chtb (
    column1 UInt32, 
    column2 String, 
    column3 String
) ENGINE=MergeTree() ORDER BY(column1);

INSERT INTO testdb.chtb SELECT * FROM testdb.costb;
```

## Using Table Function

When creating a table, you can use the `s3` built-in function to directly import data into it.
```
CREATE TABLE testdb.chtb
ENGINE=MergeTree() 
ORDER BY(column1) 
AS SELECT * FROM s3(
  'http://${bucket-name}.cos.${region}.myqcloud.com/data1.csv', 
  'CSV', 'column1 UInt32, column2 String, column3 String');
```

## References

- [CREATE Queries](https://clickhouse.tech/docs/en/query_language/create/)
- [Support S3 as the persistent storage](https://github.com/ClickHouse/ClickHouse/issues/1394)
