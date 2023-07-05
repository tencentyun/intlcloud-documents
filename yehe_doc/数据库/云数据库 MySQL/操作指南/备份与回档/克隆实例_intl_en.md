
This document describes how to clone a TencentDB for MySQL instance and quickly restore data to the newly purchased clone in the console.

## Overview
TencentDB for MySQL provides the instance cloning feature. You can now restore an instance to any point in time within the log backup retention period or from a specific physical backup set by cloning. The clone is a new instance created from the backup data according to the restoration point in time you have specified. After the clone has been verified, you can migrate its data back to the original instance with [DTS](https://intl.cloud.tencent.com/document/product/571/13709) or you can start using the clone.

#### Clone mode
- Clone an instance and restore the clone to any point in time within the log backup retention period you set.
- Clone an instance and restore the clone from a specific physical backup set within the data backup retention period you set.

#### Clone billing
- The clone adopts the pay-as-you-go billing mode. For more information on this billing mode and fee calculation, see [Billing Overview](https://intl.cloud.tencent.com/document/product/236/18335).
- The clone will not be billed until the clone process is completed.  

## Prerequisites
- Supported instance architectures: TencentDB for MySQL single-node, two-node, and three-node architectures.
- The original instance must be in **Running** status.
- If the clone mode is set to **By backup set**, the original instance must have created at least one physical backup. You can log in to the [console](https://console.cloud.tencent.com/cdb) and view the backup status on the **Backup List** tab.
- Your account balance must be positive.

## Note
- The specification of the new instance must be greater than or equal to that of the original instance.
- The hard disk space of the clone instance must be larger than the amount of the data to be cloned from, or else the clone task may fail.
- The AZ, database version, replication mode, and default database parameters of the clone must be the same as those of the original instance.
- The clone will not be displayed in the instance list in the console until the clone process is completed.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** > **Data Backup List** and click **Clone** in the top-left corner, or locate the target backup and click **Clone** in the **Operation** column.
![](https://main.qcloudimg.com/raw/b53e3c4f249a5f22638c32f4c92c7f75.png)
3. On the displayed purchase page, specify the clone mode and other configuration items and click **Buy Now**.
 - **By time point**: You can restore an instance to any time point within the log backup retention period.
 - **By backup set**: You can restore data from a backup set to a new instance. The available backup sets depend on the data backup retention period.
>?You can log in to the [console](https://console.cloud.tencent.com/cdb), select **Database Backup** on the left sidebar, and view backup retention period on the **Backup List** tab.
>
![](https://main.qcloudimg.com/raw/f2fcdd5471326b60f6ee7ea8872f00bc.png)
4. After successful purchase, you can check the clone details on the **Backup and Restoration** > **Cloned Instance List** tab.
![](https://main.qcloudimg.com/raw/3b6a2781adafd4cbde550ea00f3898a8.png)
5. After the clone process is completed, you can view the clone in the instance list.

## Relevant Documentation
- For more information on restoration of a single database or table, see [Rolling back Databases](https://intl.cloud.tencent.com/document/product/236/7276).
- For more information on how to restore data to a self-created instance, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910) and [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909).

## FAQs
#### Will the access to the source instance be affected during the clone process?
The original backup set and binlogs uploaded to COS are used for cloning, which will not affect the access to the source instance.
