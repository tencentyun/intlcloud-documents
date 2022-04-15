## Overview
This feature is used to drop tables with large data files to avoid I/O fluctuation.

`DROP TABLE` renames the original database file (.ibd) to make a new temp file and returns a success. The temp file is stored in the directory specified by the `innodb-async-drop-tmp-dir` parameter and is truncated in batches on the backend. The size of the file to be truncated each time is controlled by the `innodb-async-truncate-size` parameter. The status of the async table drop feature is controlled by the `innodb-async-drop-tmp-dir` parameter (if it is not empty, the feature will be enabled).

This feature does not require user operations and is automatically completed by the kernel. The principle is to create a hard link in another directory for the data file of the table when the table is dropped, so when `DROP TABLE` is executed, only the hard link to the file is deleted. After that, the backend thread will scan the files that need to be deleted in the hard-linked directory and automatically truncate the data file of the dropped table.

## Supported Versions
Kernel version: MySQL 5.6 20190203 and later.
Kernel version: MySQL 5.7 20190203 and later.
Kernel version: MySQL 8.0 20200630 and later.

## Use Cases
This feature is used to drop tables with large data files.

## Directions
You can set the `innodb_async_truncate_work_enabled` parameter to `ON` to enable the async mode of `DROP TABLE`. The default value is `OFF`.
The size of the file to be truncated each time is controlled by the `innodb_async_truncate_size` parameter.

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_async_truncate_work_enabled | Yes  | string |  OFF   | ON/OFF      | Whether to drop big tables asynchronously          |
| innodb_async_truncate_size         | Yes  | int    | MySQL 5.7 20210630 and earlier: 128<br>MySQL 5.7 20211030 and later: 64  | MySQL 5.7 20210630 and earlier: 128-2,048 MB<br>MySQL 5.7 20211030 and later: 16-256 MB | The size of the file to be truncated each time on the backend after the async mode of `DROP TABLE` is enabled. Unit: MB |

