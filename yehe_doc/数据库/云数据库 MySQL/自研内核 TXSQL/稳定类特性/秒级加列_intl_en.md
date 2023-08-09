
## Overview
The quick column addition feature allows you to quickly add columns to a big table by only modifying the data dictionary, which eliminates the need of data replication during column adding and greatly reduces the column adding time for big tables and the impact on the system.

## Supported Versions
- Kernel version: MySQL 5.7 20190830 and later.
- Kernel version: MySQL 8.0 20200630 and later.

## Use Cases
This feature is suitable for adding columns to a table with a high volume of data.

## Performance Data
In tests with a table of 5 GB data, the time for adding a column is reduced from 40 seconds to below 1 second.

## Instructions
- INSTANT ADD COLUMN syntax
Add the `algorithm=instant` clause to `ALTER TABLE` to add a column as follows:
```
ALTER TABLE t1 ADD COLUMN c INT, ADD COLUMN d INT DEFAULT 1000, ALGORITHM=INSTANT;
```

- The `innodb_alter_table_default_algorithm` parameter is added, which can be set to `inplace` or `instant`.
This parameter is `inplace` by default and can be configured to adjust the default algorithm of `ALTER TABLE` as follows:
```
SET @@global.innodb_alter_table_default_algorithm=instant;
```
If no algorithm is specified, the default algorithm configured by this parameter will be used for `ALTER TABLE` operations.

### Restrictions on INSTANT ADD COLUMN
- A statement can contain only column addition operations.
- A new column will be added to the end, and column order cannot be changed.
- INSTANT ADD COLUMN is not supported in tables with the COMPRESSED row format.
- INSTANT ADD COLUMN is not supported in tables with a full-text index.
- INSTANT ADD COLUMN is not supported for temp tables.
