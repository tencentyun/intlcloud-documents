
## Overview
During data consistency check, DTS compares the table data between the source and target databases and outputs the comparison result and inconsistency details for you to quickly process the inconsistent data. A data consistency check task is independent and does not affect the normal business in the source database or other DTS tasks.

A data consistency check task can be created only when the corresponding DTS task is in the **incremental sync** step.

>?Linkages currently supporting data consistency check are as follows:
>- MySQL/MariaDB/Percona/TDSQL for MySQL > MySQL 
>- MySQL/MariaDB/Percona/TDSQL for MySQL > MariaDB
>- MySQL/MariaDB/Percona > TDSQL-C for MySQL
>- MySQL/MariaDB/Percona/TDSQL for MySQL > TDSQL for MySQL
>- MySQL/MariaDB/Percona/TDSQL for TDStore > TDSQL for TDStore 

## Notes
- Data consistency compares only data migrated from the source database to the target database. If you write data into the target database during migration, then the written data will not be included in the consistency check.
- A data consistency check task may increase the load in the source database. Therefore, you need to perform such tasks during off-peak hours.
- A data consistency check task can be executed repeatedly, but one DTS instance can initiate only one such task at any time.
- A table to be checked must have a primary key or unique key; otherwise, it will be skipped by DTS during the check.
- If you choose to **complete** or **terminate** a DTS task before a data consistency check task is completed, the check task will fail.

## Restrictions
Currently, check tasks are imperceptible to the DDL operations. If you perform DDL operations in the source database during migration, the check result will be inconsistent with the actual data, and you need to initiate another check task to get the accurate comparison result.

## Creating Data Consistency Check Task
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration).
2. On the **Data Migration** page, select a migration task you want to check and click the task ID to enter the **Task Details** page.
![](https://main.qcloudimg.com/raw/d6aa1c05241017e346c11ff4cd1348ea.png)
3. Switch the tab and click **Data Consistency Check**.
<img src="https://main.qcloudimg.com/raw/30055344719ea37e3c8f1b6c45d1bc9d.png" style="zoom:50%;" />
4. Click **Create Data Consistency Check**.
>?A data consistency check task can be created only when the corresponding DTS task is in the **incremental sync** step. If the button is grayed out, the DTS task status does not meet the requirement; for example, the task has not entered the **incremental sync** step, has failed, or is terminated.
>
![](https://main.qcloudimg.com/raw/de6bc3d875d5055ec78397fce0b64560.png)
5. In the pop-up window, click **OK**.
<img src="https://main.qcloudimg.com/raw/55b8c0bc502105ea07ff7cc6988aa096.png" style="zoom:50%;" />
6. After configuring the data consistency check parameters, click **Start Data Comparison**.
You can select **All Migration Objects** or **Custom** for the migration objects.
<img src="https://main.qcloudimg.com/raw/802c91085f7d7df0021e6d71e08b404d.png" style="zoom:67%;" />

## Viewing Data Consistency Check Result
1. On the migration task homepage, click **View More** in the **Last Check Result** column.
    ![](https://main.qcloudimg.com/raw/15df5cbb4a080c17be20753d46dbdaff.png)
2. Click **View** to view the check result.
    ![](https://main.qcloudimg.com/raw/841f0c33491e71e922ce9ec86c2237f5.png)
    If the data is consistent, the result will be like:
    ![](https://qcloudimg.tencent-cloud.cn/raw/90daaff527ea15c306c72e0c20d0c355.png)<br>
    If the data is inconsistent, the result will be like:
   ![](https://qcloudimg.tencent-cloud.cn/raw/c8464bd6d8c6c7416a3407a637588815.png)

