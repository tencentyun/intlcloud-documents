## Overview

When your database instance no longer needs to be audited, disable the service in time to avoid unnecessary fees.

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
![](https://qcloudimg.tencent-cloud.cn/raw/241e70bad336f3696b01a81b17c2f8c0.png)
7. In the pop-up window, select **Disable service** after **Log Retention Period** and click **Submit**.
> ?In order to meet the security compliance requirements for the retention period of audit logs, we recommend you select 180 days or above.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/cec32d97450dfd3b160d1eb74b64df83.png)

