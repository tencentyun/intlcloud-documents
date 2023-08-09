## Overview
This feature is used to drop tables with large data files to avoid I/O fluctuation.

`DROP TABLE` renames the original database file (.ibd) to make a new temp file and returns a success. The temp file is stored in the directory specified by the `innodb_async_drop_tmp_dir` parameter and is truncated in batches on the backend. The size of the file to be truncated each time is specified by the `innodb_async_truncate_size` parameter. The status of the async table drop feature is controlled by the `innodb_async_truncate_work_enabled` parameter.

This feature does not require user operations and is automatically completed by the kernel. The principle is to create a hard link in another directory for the data file of the table when the table is dropped, so when `DROP TABLE` is executed, only the hard link to the file is deleted. After that, the backend thread will scan the files that need to be deleted in the hard-linked directory and automatically truncate the data file of the dropped table.

## Supported Versions
- Kernel version: MySQL 5.6 20200303 and later.
- Kernel version: MySQL 5.7 20220715 and later.
- Kernel version: MySQL 8.0 20200630 and later.

## Use Cases
This feature is used to drop tables with large data files.

## Instructions
- For MySQL 5.6, you can set the `innodb_async_truncate_work_enabled` parameter to `ON` to enable the async mode of `DROP TABLE`. The default value is `OFF`.
- For MySQL 5.7 and 8.0, you can set the `innodb_table_drop_mode` parameter to `ASYNC_DROP` to enable the async mode of `DROP TABLE`. The default value is `SYNC_DROP`.
- The size of the file to be truncated each time is specified by the `innodb_async_truncate_size` parameter. This is not supported for MySQL 5.6.
- You can make the async drop of big tables more efficient by enabling the `innodb_fast_ddl` parameter as instructed in [FAST DDL](https://intl.cloud.tencent.com/document/product/236/43489).

<dx-tabs>
::: MySQL 5.6 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_async_truncate_work_enabled | Yes | string | OFF | ON/OFF | Whether to drop big tables asynchronously.           |
:::
::: MySQL 5.7 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_table_drop_mode | Yes | string | SYNC_DROP | SYNC_DROP/ASYNC_DROP | Whether to drop big tables asynchronously.           |
| innodb_async_truncate_size | Yes | int | 128 | 128–168 |The size of the file to be truncated each time on the backend after the async mode of `DROP TABLE` is enabled. Unit: MB.  |
:::
::: MySQL 8.0 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_table_drop_mode | Yes | string | SYNC_DROP | SYNC_DROP/ASYNC_DROP | Whether to drop big tables asynchronously.          |
| innodb_async_truncate_size | Yes | int | 128 | 128–168 |The size of the file to be truncated each time on the backend after the async mode of `DROP TABLE` is enabled. Unit: MB. |
:::
</dx-tabs>
