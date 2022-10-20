## Overview

TencentDB for MongoDB's audit service supports long-term retention of audit logs. You can adjust the retention period at any time based on the security compliance requirements of your business audit rules.

## Prerequisites

- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551) and enabled database audit for it.
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance with **Audit Status** being **Enabled**.
5. Click the instance ID to enter the **Audit Log** tab and view audit logs.
6. In the top-right corner of the **Audit Log** tab, click **Configure**.
![](https://qcloudimg.tencent-cloud.cn/raw/e4d6404a7800c33bb1256859d21b772e.png)
7. In the pop-up window, modify the log retention period and click **Submit**.
> ?In order to meet the security compliance requirements for the retention period of audit logs, we recommend you select 180 days or above.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/66dace29c5ea763aef3bff6b5639524d.png)

