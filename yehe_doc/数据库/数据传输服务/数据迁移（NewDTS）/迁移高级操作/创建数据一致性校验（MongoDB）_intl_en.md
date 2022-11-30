
## Overview
During data consistency check, DTS compares the table data between the source and target databases and outputs the comparison result and inconsistency details for you to determine the business cutover time. A data consistency check task is independent of the normal business in the source database or other DTS tasks.

Data consistency check tasks can be triggered automatically or created manually.

- Automatic triggering: During migration task configuration, if **Full check** is selected for **Data Consistency Check**, a data consistency check task will be triggered automatically when the migration task enters the **incremental sync** step.
- Manual creation: When the DTS task enters the **incremental sync** step, you can manually create one or multiple data consistency check tasks.

## Notes
- Data consistency check compares only the objects selected in the source database and objects migrated to the target database. If you write data into the target database during migration, then the written data will not be included in the consistency check.
- A data consistency check task may increase the load in the source database instance. Therefore, you need to perform such tasks during off-peak hours.
- A data consistency check task can be executed repeatedly, but one DTS instance can initiate only one such task at any time.
- If you choose to **complete** or **terminate** a DTS task before a data consistency check task is completed, the check task will fail.
- As data consistency check requires creating a new database `__tencentdb__` in the source database and writing the checksum table to the database, if the source database is read-only, data consistency check will be skipped. 

## Restrictions
Currently, check tasks are imperceptible to the DDL operations. If you perform DDL operations in the source database during migration, the check result will be inconsistent with the actual data, and you need to initiate another check task to get the accurate comparison result.

## Triggering a data consistency check task automatically

On the **Set migration options and select migration objects** page of a [data migration task](https://console.cloud.tencent.com/dts/migration), select **Full check** for **Data Consistency Check**. In this way, a data consistency check task will be triggered automatically when the migration task enters the **incremental sync** step.
> ?In this case, the full data and all the database information will be checked by default. If you need to filter check objects, create a data consistency check task manually.



## Creating a data consistency check task manually

1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration).
2. On the **Data Migration** page, select the target migration task and click **More** > **Create Data Consistency Check Task** in the **Operation** column.

3. Click **Create Data Consistency Check**.
>?A data consistency check task can be created only when the corresponding DTS task is in the **incremental sync** step. If the button is grayed out, the DTS task status does not meet the requirement; for example, the task has not entered the **incremental sync** step, has failed, or is terminated.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ee3616aae11c9f83adf25c902db03c09.png)
4. In the pop-up window, click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7f8dfed208808b5fd3fb3805541becaf.png" style="zoom:90%;" />
5. After configuring the data consistency check parameters, click **Start Data Comparison**.
 - Check Object: Select **All Migration Objects** or **Custom**.
 - Database Information: Select **Index**, **Shard key** (if both the source and target databases are sharded clusters), or **Database and table** for check.
 - Data Check: The **Row count check** option compares the number of data rows in the source and target databases. The **Content check** option compares the data content of the source and target databases.
 - Sampling Percentage: In scenarios with a high data volume, extracting all the data for check may increase the load of the source database. If you select **Content check**, you can set an appropriate percentage based on your business conditions to extract a certain proportion of data for comparison.
![](https://qcloudimg.tencent-cloud.cn/raw/33f22832c023c6e5c823482cba5ae8fe.png)

## Viewing the data consistency check result
1. On the migration task homepage, view whether the check result is **Consistent** or **Inconsistent** in the **Last Check Result** column. Click **View More** to enter the **Verification Details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/c43043ec0d950c05a9703f173c8659e9.png)   
2. Click **View** to view the check result.
![](https://qcloudimg.tencent-cloud.cn/raw/d29df913b865c78894eb626162540a2c.png)
**If the data is consistent, the result will be like:**
![](https://qcloudimg.tencent-cloud.cn/raw/d3240dd21121889c53285e590fc32b13.png)<br>

