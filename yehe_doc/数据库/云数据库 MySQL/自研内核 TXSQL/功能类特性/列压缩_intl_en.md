## Overview
Row compression and data page compression are already supported, but if small fields in a table are read and written frequently while big fields are not, both of the compression methods waste a lot of computing resources.

In contrast, column compression can compress big fields that are infrequently accessed while ignoring the frequently accessed small fields, which not only reduces the space for storing whole rows of fields but also improves the read and write access efficiency.

For example, in the employee table `create table employee(id int, age int, gender boolean, other varchar(1000) primary key (id))`, if access is frequent for small fields such as `id`, `age`, and `gender` but infrequent for the large field `other`, you can compress the `other` column. Generally, only read/write of the `other` column rather than other columns will trigger the compression and decompression of this column, which further reduces the size of the stored row data. In this way, frequently accessed small fields can be accessed more quickly, while infrequently accessed large fields can be compress to use less storage space.

## Supported Versions
Kernel version: MySQL 5.7 20210330 and above.
>? Column compression for closed by default, if you want to use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to open. 
## Use Cases
If a table has many frequently accessed small fields and infrequently accessed large fields, you can compress the large field columns.

## Instructions
### Supported data types
1. `BLOB` (including `TINYBLOB`, `MEDIUMBLOB`, and `LONGBLOB`)
2. `TEXT` (including `TINYTEXT`, `MEDIUMTEXT`, and `LONGTEXT`)
3. `VARCHAR`
4. `VARBINARY`

>!Here, the maximum length of `LONGBLOB` and `LONGTEXT` is $2^{32}-2$ bytes, which is one byte less than $2^{32}-1$ supported by native MySQL as described in [String Type Storage Requirements](https://dev.mysql.com/doc/refman/5.7/en/storage-requirements.html).

### Supported DDL syntax types
Different from the [table creation syntax](https://dev.mysql.com/doc/refman/5.7/en/create-table.html) of native MySQL, the definition of `COLUMN_FORMAT` in `column_definition` is changed in TencentDB for MySQL. In addition, column compression is supported only for tables with the InnoDB storage engine.
```sql
      column_definition:
        data_type [NOT NULL | NULL] [DEFAULT default_value]
          [AUTO_INCREMENT] [UNIQUE [KEY]] [[PRIMARY] KEY]
          [COMMENT 'string']
          [COLLATE collation_name]
          [COLUMN_FORMAT {FIXED|DYNAMIC|DEFAULT}|COMPRESSED=[zlib]]  # `COMPRESSED` is the compressed column keyword
          [STORAGE {DISK|MEMORY}]
          [reference_definition]
```

Below is a simple example:
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED
);
```

Here, as the compression algorithm is not specified, the `zlib` algorithm will be selected by default. You can also specify the compression algorithm keyword, but only `zlib` is supported currently.
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED=zlib
);
```

The following DDL syntaxes are supported:
**CREATE TABLE:**

| DDL                                         | Whether the Compression Attribute is Inherited |
| ------------------------------------------- | ---------------- |
| `CREATE TABLE t2 LIKE t1;`                  | Yes                |
| `CREATE TABLE t2 SELECT * FROM t1;`         | Yes                |
| `CREATE TABLE t2(a BLOB) SELECT * FROM t1;` | No                |

**ALTER TABLE:**

| DDL                                               | Description                 |
| ------------------------------------------------- | -------------------- |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB;`            | Alters a compressed column into a non-compressed one |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB COMPRESSED;` | Alters a non-compressed column into a compressed one |

 
### New variable description

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| --------------------------------------- | ---- | ------- | ---- | --------------- | ------------------------------------------------------------ |
| innodb_column_compression_zlib_wrap     | Yes  | bool    | TRUE | TRUE/FALSE   | If it is set to `TRUE`, the data zlib header and tail will be generated, and Adler-32 check will be performed.    |
| innodb_column_compression_zlib_strategy | Yes  | Integer | 0    | [0, 4]           | Column compression policy. Valid values: 0: Z_DEFAULT_STRATEGY; 1: Z_FILTERED; 2: Z_HUFFMAN_ONLY; 3: Z_RLE; 4: Z_FIXED. <br>Generally, `Z_DEFAULT_STRATEGY` is the best choice for text data, while `Z_RLE` for image data. |
| innodb_column_compression_zlib_level    | Yes  | Integer | 6    | [0, 9]           | Column compression level. Value range: 0–9. 0 indicates not to compress. The higher the value, the smaller the data size after compression, and the longer the compression duration. |
| innodb_column_compression_threshold     | Yes  | Integer | 256  | [0, 0xffffffff] | Column compression threshold in bytes. Value range: 1–0xffffffff. Only data whose length is at or above this threshold will be compressed; otherwise, the original data will stay unchanged with only a compression header added. |
| innodb_column_compression_pct           | Yes  | Integer | 100  | [1, 100]        | Column compression ratio in percentages. Value range: 1–100. Data will be compressed only if the **data size after compression/data size before compression** is below this value; otherwise, the original data will stay unchanged with only a compression header added. |

>?Currently, you cannot directly modify the values of the above parameters. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

### New status description

| Name                         | Type    | Description                                                |
| ---------------------------- | ------- | ---------------------------------------------------------- |
| `Innodb_column_compressed`   | Integer | Number of column compressions, including compressions for non-compressed data and compressed data.   |
| `Innodb_column_decompressed` | Integer | Number of column decompressions, including decompressions for non-compressed data and compressed data. |

### New error description

| Name                                                         | Scope                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ |
| `Compressed column '%-.192s' can't be used in key specification` | Name of the column specified for compression                  | The compression attribute cannot be specified for a column with an index.                                 |
| `Unknown compression method: %s"`                            | Name of the compression algorithm specified in the DDL statement | An invalid compression algorithm other than `zlib` is specified in the `CREATE TABLE` or `ALTER TABLE` statement. |
| `Compressed column '%-.192s' can't be used in column format specification` | Name of the column specified for compression                  | If the `COLUMN_FORMAT` attribute has been specified for a column, other attributes cannot be specified, and `COLUMN_FORMAT` can be used only in NDB. |
| `Alter table ... discard/import tablespace not support column compression` | \                 | The `ALTER TABLE ... DISCARD/IMPORT TABLESPACE` statement cannot be executed for tables with column compression enabled. |

### Performance
The performance varies by DDL and DML statements:
For DDL statements, sysbench is used for testing:
- Column compression compromises much performance of DDL statements with the COPY algorithm, and the performance after compression is 7–8 times lower than before.
- The impact of column compression on INPLACE DDL statements is subject to the data volume after compression. If the overall data size is reduced after compression, the DDL performance will be improved; otherwise, it will be compromised.
- Column compression almost has no impact on INSTANT DDL statements.

For DML statements, in an 8-column table with the most common compression ratio of 1:1.8 (where the length of the inserted data varies randomly from 1 to 6,000, the inserted characters are random within 0–9 and a–b, a column contains a large volume of varchar data, and the data types of other columns are either char(60) or int), the performance of insertion, deletion, and query of non-compressed columns in this table is improved by below 10%, but the performance of update of non-compressed and compressed columns is reduced by below 10% and 15% respectively. This is because that TencentDB for MySQL first reads the value of a row and then writes the updated value, which triggers one decompression/compression process, while insertion and query only trigger one compression or decompression.

### Notes
1. During logic export, CREATE TABLE statements will carry the `COMPRESSED` keyword. Therefore, TencentDB for MySQL supports such statements during import. Below are notes on official MySQL versions:
   - If the official MySQL version is below 5.7.18, data can be imported directly.
   - If the official MySQL version is 5.7.18 or above, the `COMPRESSED` keyword must be removed after logic export.
2. When DTS exports data from other cloud service providers or users, incompatibility may occur during binlog sync. In this case, you can skip DDL statements with the `COMPRESSED` keyword.

