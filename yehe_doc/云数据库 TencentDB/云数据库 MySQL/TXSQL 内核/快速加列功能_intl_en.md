This document describes how to quickly add columns in big tables through the `instant` algorithm while avoiding data replication This feature does not replicate the data or use disk space/IO and can implement changes during peak hours.

## Prerequisites
- Instance version: MySQL 5.7 High-Availability Edition and Finance Edition
- Kernel minor version: 20190830 and above
>Newly purchased instances are on the latest kernel version by default. For more information on how to view the kernel version, please see [Viewing Kernel Version Number](https://intl.cloud.tencent.com/document/product/236/35995). For more information on the kernel updates, please see [Kernel Version Updates](https://intl.cloud.tencent.com/document/product/236/35989).

## Directions
[Log in to the database](https://intl.cloud.tencent.com/document/product/236/3130) and use the following syntax to quickly add a column.
```
ALTER TABLE t1 ADD COLUMN c1 int, algorithm=instant;
```
>
>- The `innodb_alter_table_default_algorithm` parameter is used to specify the default `ALTER TABLE` algorithm. If it is set to `INSTANT`, there is no need to specify the `algorithm=instant` syntax for `ALTER TABLE`. Currently, you cannot directly modify the default value of this parameter. If you want to modify it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>- The `innodb_alter_table_default_algorithm` parameter can be set to `INPLACE` (default value) or `INSTANT`.
