
This document describes how to use the `instant` algorithm to quickly add columns in big tables, while avoiding data replication. This feature does not replicate the data or use disk capacity/IO, and can implement changes in real time during peak hours.

## Limits
- Supported instance architecture and version: two-node or three-node MySQL v5.7
- Supported kernel minor version: 20190830 and later
>?Newly purchased instances use the latest kernel minor version by default. For more information on how to view the kernel minor version, see [How do I check the kernel minor version?](https://intl.cloud.tencent.com/document/product/236/35995). For more information on kernel updates, see [Kernel Version Updates](https://intl.cloud.tencent.com/document/product/236/35989).

## Directions
[Log in to the database](https://intl.cloud.tencent.com/document/product/236/37788) and use the following syntax to quickly add a column:
```
ALTER TABLE t1 ADD COLUMN c1 int, algorithm=instant;
```
>?
>- The `innodb_alter_table_default_algorithm` parameter is used to specify the default `ALTER TABLE` algorithm. If `INSTANT` is configured, there is no need to specify the `algorithm=instant` syntax for `ALTER TABLE`. Currently, you cannot directly modify the default value of this parameter. To modify it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- The `innodb_alter_table_default_algorithm` parameter can be configured as `INPLACE` (default value) or `INSTANT`.
