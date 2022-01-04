## Feature Overview
This feature is used to delete tables with large data files to avoid I/O fluctuation.
The DROP TABLE statement renames the to-be-deleted .ibd file to a temp file, returns success message, and then truncates the temp file in batches at the backend.

## Supported Versions
Kernel version: MySQL 5.7 20190203 and above.

## Use Cases
This feature is used to delete tables with large data files.

## Use Instructions
You can set the `innodb_async_truncate_work_enabled` parameter to `ON` to enable the async mode of DROP TABLE. The default value is `OFF`.
The temp file is stored in the directory specified by the `innodb_async_drop_tmp_dirr` parameter. The size of the file to be truncated each time is controlled by the `innodb_async_truncate_size` parameter.

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_async_truncate_work_enabled | Yes  | string |  OFF   | ON/OFF      | Whether to delete big tables asynchronously          |
| innodb_async_truncate_size         | Yes  | int    | MySQL 5.7 20210630 and below: 128<br>MySQL 5.7 20211030 and above: 64  | MySQL 5.7 20210630 and below: 128-2,048 MB<br>MySQL 5.7 20211030 and above: 16-256 MB | The size of the file to be truncated each time at the backend after the async mode of DROP TABLE is enabled. Unit: MB |

