## Overview
This feature kills transactions that have been idle for the specified time period to release resources in time.

## Supported Versions
- Kernel version: MySQL 5.6 20180915 and above.
- Kernel version: MySQL 5.7 20180918 and above.
- Kernel version: MySQL 8.0 20200630 and above.

## Use Cases
If a connection starts a transaction (explicitly using `begin`/`start transaction` or implicitly) but no new statement has been executed for the specified threshold period, the connection will be killed.

## Instructions
Use the `cdb_kill_idle_trans_timeout` parameter to enable or disable the feature. If it is `0`, the feature is disabled; otherwise, a connection idle for `cdb_kill_idle_trans_timeout` or `wait_timeout` seconds, whichever is smaller, will be killed. (`wait_timeout` is a session parameter.)

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| --------------------------- | ---- | ----- | ---- | ------------- | ------------------------------------------------------------ |
| cdb_kill_idle_trans_timeout | Yes  | ulong | 0    | [0, 31536000] | If it is `0`, the feature is disabled; otherwise, a transaction idle for `cdb_kill_idle_trans_timeout` seconds will be killed. |

>?Currently, you cannot directly modify the values of the above parameter. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
