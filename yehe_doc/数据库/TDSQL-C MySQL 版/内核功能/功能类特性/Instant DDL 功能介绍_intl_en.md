## Use Cases
This feature can use DDL operations to alter ultra big tables in online businesses within seconds.
 
## Description
The instant DDL feature can quickly modify columns in big tables while avoiding data replication. This feature does not replicate the data or consume disk capacity or I/O, and can implement changes within seconds during peak hours.

## Supported Versions
- MySQL 5.7 with kernel minor version 2.0.13 or later.
- MySQL 8.0 with kernel minor version 3.1.1 or later.

## Instructions
Instant DDL supports the following operations:
- ADD COLUMN
- MODIFY COLUMN

### INSTANT ADD COLUMN operation description
1. INSTANT ADD COLUMN syntax
Add the `algorithm=instant` clause to `ALTER TABLE` to add a column as follows:
```
ALTER TABLE t1 ADD COLUMN c INT, ADD COLUMN d INT DEFAULT 1000, ALGORITHM=INSTANT;
```
2. The `innodb_alter_table_default_algorithm` parameter is added, which can be set to `inplace` or `instant`.
This parameter is `inplace` by default and can be configured to adjust the default algorithm of `ALTER TABLE` as follows:
```
SET @@global.innodb_alter_table_default_algorithm=instant;
```
If no algorithm is specified, the default algorithm configured by this parameter will be used for `ALTER TABLE` operations.

#### Restrictions on INSTANT ADD COLUMN
- A statement can contain only column addition operations.
- A new column will be added to the end, and column order cannot be changed.
- INSTANT ADD COLUMN is not supported in tables with the row format being COMPRESSED.
- INSTANT ADD COLUMN is not supported in tables with a full-text index.
- INSTANT ADD COLUMN is not supported for temp tables.


### INSTANT MODIFY COLUMN operation description
1. Its usage is similar to that of INSTANT ADD COLUMN. You can set `innodb_alter_table_default_algorithm=instant` or specify the `ALGORITHM=instant` keyword when modifying a column.
```
ALTER TABLE t1 MODIFY COLUMN c BIGINT, ALGORITHM=INSTANT;
```
2. The `cdb_instant_modify_column_enabled` switch parameter is added, and the above parameters can take effect only after the switch is on. If the switch is off, the INSTANT MODIFY COLUMN feature will also be disabled.
>!After the switch is turned off, tables modified with INSTANT MODIFY COLUMN can be used normally.

#### Restrictions on INSTANT MODIFY COLUMN
- INSTANT MODIFY COLUMN supports modifying only the column type. It supports modifying the `default` attribute of fields but not the `nullable`, `unsigned/signed`, and `charset` attributes.
- Modification is supported only for certain types, and the length can be increased only. Currently, conversions between `char` and `varchar`, between `binary` and `varbinary`, and among `tinyint`, `smallint`, `mediumint`, `int`, and `bigint` are supported.
- One column can be modified with INSTANT MODIFY COLUMN only once, and multiple columns can be modified with it at the same time. After a column is added/modified with INSTANT ADD/MODIFY COLUMN for the first time, it can be modified only in the non-instant manner.
- You can run INSTANT ADD COLUMNS and INSTANT MODIFY COLUMNS separately. You can run INSTANT ADD COLUMNS first and then run INSTANT MODIFY COLUMNS or vice versa. However, you cannot perform INSTANT MODIFY COLUMN on a column that is added with INSTANT ADD COLUMN.
- You cannot modify the column name and column type at the same time. Instead, you can modify the column name first and then column type.
- INSTANT MODIFY COLUMN does not support import/export and index column modification.
- INSTANT MODIFY COLUMN does not support encryption, storage, and redundant format.

## Effect Comparison
- INSTANT ADD COLUMN and INSTANT MODIFY COLUMN are performed on the same table with about 50 million data records (around 12 GB). As can be seen, normal column addition and modification take 2 and 21 minutes respectively, while INSTANT ADD COLUMN and INSTANT MODIFY COLUMN can be done almost instantly, implementing changes within seconds.
<img src="https://main.qcloudimg.com/raw/d50bdfe19657d955204ba8fc8331d277.png"  style="zoom:80%;">


 
