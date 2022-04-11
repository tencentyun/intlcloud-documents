This document describes how to clone a TencentDB for PostgreSQL instance in the console. This feature enables you to quickly restore original instance data from a backup to a newly purchased instance.

## Overview
You can restore a TencentDB for PostgreSQL instance to any time point within the log backup retention period or from a specific physical backup set through instance clone. The clone is a new instance created from the backup data according to the restoration time point you specify. After the clone is verified, you can migrate its data back to the original instance with [DTS](https://intl.cloud.tencent.com/document/product/571/13709) or directly use the clone.

### Clone mode
- Clone an instance and restore the clone to any time point within the log backup retention period you specify.
- Clone an instance and restore the clone from a specific physical backup set within the data backup retention period you specify.

### Clone billing
- You can select a billing mode for the clone during the clone process in the same way as during instance purchase.
- The clone will not be billed until the clone process is completed.  

## Prerequisites
- The original instance must be in the **Running** status.
- If the clone mode is set to **By backup set**, the original instance must have created at least one physical backup. You can log in to the [console](https://console.cloud.tencent.com/postgres), select **Database Backup** on the left sidebar, and view backup status on the **Backup List** tab.
- Your account balance must be positive.

## Notes
- The hard disk space of the clone must be larger than the amount of the data to be cloned from; otherwise, the clone task may fail.
- The database version of the clone must be the same as that of the original instance.
- For instances with a used capacity greater than 6 TB, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for data restoration.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** > **Backup List** and click **Clone** in the top-left corner, or locate the target backup and click **Clone** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/618a51a52a6f0084189c522e44457d81.png)
3. On the displayed purchase page, specify the clone mode and other configurations and click **Buy Now**.
 - **By time point**: You can restore an instance to any time point within the past seven days.
 - **By backup set**: You can restore data from a backup set to a new instance. The available backup sets depend on the data backup retention period.
>?You can log in to the [console](https://console.cloud.tencent.com/postgres), select **Database Backup** on the left sidebar, and view backup retention period on the **Backup List** tab.
>
![](https://qcloudimg.tencent-cloud.cn/raw/26a8437e69e0731141b9cbabf72ffa00.png)
4. After successful purchase, you can view the details of the clone on the instance list page.


## FAQs
#### Will the access to the original instance be affected during the clone process?
The original backup set and log files uploaded to COS are used for restoration, which will not affect the access to the original instance.
