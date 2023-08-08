## Overview
The `fsync()` system call flushes redo logs to disk, including metadata and data. But metadata contains unimportant information such as the last modified time. You can enable the `fdatasync()` system call to skip metadata when flushing redo logs in order to reduce costs.

## Supported Versions
- Kernel version: MySQL 5.7 20201230 and above.
- Kernel version: MySQL 8.0 20201230 and above.

## Use Cases
This feature is suitable for use cases with heavy write pressure.

## Performance Data
TPS is improved by about 10%, according to the sysbench test in a high-concurrency continuous write scenario using the oltp_write_only.lua script.

## Instructions
Use the `innodb_flush_redo_using_fdatasync` parameter to enable or disable `fdatasync()`. Valid values: `true` (enable), `false` (disable). Default value: `false`. If `fdatasync()` is enabled, metadata of redo logs won't be flushed to disk in real time.

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| --------------------------------- | ---- | ---- | ----- | ---------- | --------------------------- |
| innodb_flush_redo_using_fdatasync | Yes  | bool | false | true/false | Whether to call `fdatasync()` to flush redo logs |

