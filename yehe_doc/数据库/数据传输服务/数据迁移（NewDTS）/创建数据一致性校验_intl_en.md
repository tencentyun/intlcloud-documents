
## Overview
During data consistency check, DTS compares the table data between the source and target databases and outputs the comparison result and inconsistency details for you to quickly process the inconsistent data. A data consistency check task is independent and does not affect the normal business in the source database or other DTS tasks.

A data consistency check task can be created only when the corresponding DTS task is in the **incremental sync** step.

>?Currently, data consistency check is supported only for migration from self-built MySQL, TencentDB for MySQL, and third-party MySQL to TencentDB for MySQL/TDSQL-C.

## Notes
- Data consistency compares only data migrated from the source database to the target database. If you write data into the target database during migration, then the written data will not be included in the consistency check.
- A data consistency check task may increase the load in the source database. Therefore, you need to perform such tasks during off-peak hours.
- A data consistency check task can be executed repeatedly, but one DTS instance can initiate only one such task at any time.
- A table to be checked must have a primary key or unique key; otherwise, it will be skipped by DTS during the check.
- If you choose to **complete** or **terminate** a DTS task before a data consistency check task is completed, the check task will fail.

## Restrictions
Currently, check tasks are imperceptible to the DDL operations. If you perform DDL operations in the source database during migration, the check result will be inconsistent with the actual data, and you need to initiate another check task to get the accurate comparison result.

## Directions
#### Creating data consistency check task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration).
2. On the **Data Migration** page, select a migration task you want to check and click the task ID to enter the **Task Details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/0af144b0e8cb179934b28c2c45d567e2.png)
3. Switch the tab and click **Data Consistency Check**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/976fc2ce2f0374756b923134dda370d9.png" style="zoom:50%;" />
4. Click **Create Data Consistency Check**.
>?A data consistency check task can be created only when the corresponding DTS task is in the **incremental sync** step. If the button is grayed out, the DTS task status does not meet the requirement; for example, the task has not entered the **incremental sync** step, has failed, or is terminated.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ee3616aae11c9f83adf25c902db03c09.png)
5. In the pop-up window, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b785c2ca36159ead67d9a72bc9c910e9.png)
6. After configuring the data consistency check parameters, click **Start Data Comparison**.
You can select **All Migration Objects** or **Custom** for the migration objects.
![](https://qcloudimg.tencent-cloud.cn/raw/33f22832c023c6e5c823482cba5ae8fe.png)

#### Viewing data consistency check result
1. On the migration task homepage, click **View More** in the **Last Check Result** column.
2. Click **View** to view the check result.
![](https://qcloudimg.tencent-cloud.cn/raw/1c0f1f80e884f70371b8de3cce0b9296.png)
If the data is consistent, the result will be like:
![](https://qcloudimg.tencent-cloud.cn/raw/01651c2a2edb7dc770e04b2ffd5fe6ba.png)

