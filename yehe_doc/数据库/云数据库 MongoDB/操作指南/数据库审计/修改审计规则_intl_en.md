## Overview

TencentDB for MongoDB's audit service allows you to adjust audit rules at any time based on your business scenario to ensure efficient, accurate, and compliant audit of databases.


## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551) and enabled database audit for it.
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance with **Audit Status** being **Enabled**.
5. Click the search box and find the target instance by **Instance ID**, **Instance Name**, **Tag Key**, or **Tag** in the drop-down list.
6. In the **Audit Rule** column of the target instance, click <img src="https://qcloudimg.tencent-cloud.cn/raw/6d83c4493e2005a00dee8edeb82d8e6a.png" style="zoom:67%;" />.
7. In the **Audit Rule** panel displayed on the right, you can modify the mode of an **audit rule** by selecting full audit or rule audit.
8. For **rule audit**, you can reset the audit rule as prompted. You should separate SQL type, database name, collection name, client IP, and username by comma.
![](https://qcloudimg.tencent-cloud.cn/raw/893f8a9959a3a1d59f3c4490c7ff1fa2.png)
9. Click **Save**, and databases will be audited based on the new audit rule.

## More operations
For more information on database audit operations, see [Viewing Audit Log](https://intl.cloud.tencent.com/document/product/1102/47772).

