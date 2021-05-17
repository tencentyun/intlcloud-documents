This document describes how to synchronize data from TencentDB for MySQL to Cloud Data Warehouse PostgreSQL (CDWPG).

CDWPG is Tencent Cloud’s big data warehouse product. Through DTS, CDWPG enables you to synchronize data from TencentDB for MySQL to it in real time and realize data closed loop from TP (online transaction processing) databases to AP (online analytical processing) databases.

## Prerequisites
- You have [created a TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/37785). Supported MySQL versions: v5.6 and v5.7.
- You need to create a migration account on the source MySQL instance. Account permissions required are as follows:
```
GRANT RELOAD,LOCK TABLE,REPLICATION CLIENT,REPLICATION SLAVE,SELECT ON *.* TO "migration account"@"%" IDENTIFIED BY "migration password";
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO "migration account"@"%";
FLUSH PRIVILEGES;
```
- You have [created a CDWPG instance](https://cloud.tencent.com/document/product/878/31447). Supported CDWPG version: v1.0.0.
- You need to create a migration account on the target CDWPG instance. Account permissions required are as follows:
```
Delete
Truncate
Insert
References
Select
Update
TRIGGER
```
- To configure a data sync task between TencentDB for MySQL to CDWPG, you need to perform precheck before starting the task. The main check items are described below:

| Check Items | Description |
| ------------------------------ | ------------------------------------------- |
| Check whether `schema` and `table` exist in the target database | You need to create `schema` and `table` in advance. Otherwise, an error will be reported |
| Check whether the current user has permissions for target database tables | To synchronize a table, you need to first check whether the current user is the table owner, who has all the permissions required. If not, please check the permission information in the `information_schema.table_privilege` table and make sure the following permissions, including `Delete`, `Truncate`, `Insert`, `References`, `Select`, `Update`, and `TRIGGER`, are granted. Otherwise, an error will be reported |
| Check whether the target database has sufficient disk space | Compare the target database’s available disk space and the space the source database needs |
| Check source database permissions | Check whether the source instance has the following permissions: `Reload`, `LockTable`, `ReplClient`, `ReplSlave`, `Select`, and `REPLICATION CLIENT` |
| Check the parameter `connect_timeout’ of the source MySQL instance | Check whether this parameter is less than 10. If so, an error will be reported |
| Check the connectivity of the source and target databases | Check whether the MySQL and CDWPG instances can be correctly connected |
| Check MySQL versions | The version of the source MySQL instance must be MySQL 5.6 or MySQL 5.7 |
| Check source instance optimization parameter | You need to disable the metric `innodb_stats_on_metadata` |
| Check source instance binlog parameter | The parameter `binlog_format` must be `ROW`；`binlog_row_image` must be `FULL`；`log_bin` must be `ON`；`gtid_mode` must be `ON` |
| Check primary key constraint | Tables to be synchronized in the source database must have primary keys |
| Check source database code | The code must be `utf8` or `utf8mb4` |
| Check case configuration of MySQL table names | Check whether the parameter `lower_case_table_names` is 0. If not, the configuration is incorrect |
| Check whether the MySQL database table name or column name contains `"` | CDWPG does not support column names with `"` |

## Notes
- When DTS performs full data migration, it will occupy certain source instance resources, which may increase the load of the source instance and the database pressure. If your database has low configurations, we recommend that you migrate data during off-peak hours.
- Tables to be synchronized in the TencentDB for MySQL instance must have primary keys.

## SQL Operations Supported for Sync
DML operations, including `INSERT`, `UPDATE`, `DELETE`, and `REPLACE`, in source database tables can be synchronized.

## Architectures Supported for Sync
- One-to-one one-way sync.
- One-to-many one-way sync.
- Many-to-one one-way sync.

## Directions
1. Log in to the [data sync purchase page](https://buy.cloud.tencent.com/dts), select corresponding configurations and click **Buy Now**
 - Billing Mode: you can either select “Monthly subscription” or “Pay-as-you-go”. Data sync services are free of charge currently. Once they are charged, we will notify you via email and Message Center 1 month in advance.
 - Source Instance Type: you can only select “MySQL” currently.
 - Source Instance Region: you cannot modify the region you have selected. Please select the region where the source instance resides.
 - Target Instance Type: you can only select “CDWPG” currently.
 - Target Instance Region: please select the region where the target instance resides. You cannot modify the region you have selected. 
 - Sync Task Specification: you can only select “Standard Edition” currently.
2. Confirm information in the pop-up dialogue box and click **Buy Now**. You can return to the data sync list to view the newly created data sync task. You need to configure this task before running it.
3. On the [Data Sync List](https://console.cloud.tencent.com/dts/replication) page, click **Configuration** in the “Operation” column to enter the data sync task configuration page.
4. On the page you enter, configure the source instance, account and password, as well as the target instance, account and password. After the connectivity test is passed, click **Next**.
 - Task Name: DTS will automatically generate a task name. You can modify it as needed.
 - Running Mode: you can either select “Immediate execution” or “Scheduled execution”.
 - Source Instance Type: you cannot modify the TencentDB for MySQL instance type you have selected.
 - Source Instance Region: you cannot modify the selected region of the TencentDB for MySQL instance.
 - Access Type: you can only select TencentDB currently.
 - Instance ID: select the source instance ID.
 - Source database account and password: enter the actual [database account and password](https://intl.cloud.tencent.com/document/product/236/31901) and click **Test Connectivity**.
 - Target Instance Type: you cannot modify the target instance type you have selected.
 - Target Instance Region: you cannot modify the selected target instance region.
 - Access Type: you can only select “CDWPG” currently.
 - Instance ID: select the target instance ID.
 - Database Name: the name of the CDWPG database where data is synchronized to.
 - Target database account and password: enter the actual [database account and password](https://console.cloud.tencent.com/cdwpg) and click **Test Connectivity**.
5. On the “Set sync options and objects” page, select corresponding configurations and click **Save and Go Next**.
 - Initialization: you can only select “Full data initialization” currently.
 - If Target Already Exists: you can select from the two policies: “Delete and reinitialize” and “Append to existing”.
    - Delete and reinitialize: if tables with the same name exist in the target database, data in these tables will be deleted before reinitialization.
    - Ignore and execute: the “full data initialization” option will add full data, which is suitable for integrating multiple tables into one.
 - SQL Type: only DML operations are supported now.
 - Sync Object: select tables to be migrated from the source database.
6. On the “Verify task” page, click **Start Task** after all the items are successfully verified.
7. Return to the data sync task list, and the task will be in the “Running” status.
 - If you click “Pause”, data sync will pause. You can click **Start** to continue with the data sync task.
 - If you click “Stop”, the task will be closed. Please make sure data sync is completed before closing the task.
 - You can reset the task when it is in the pause status. After that, the synchronized information will not be retained. Please proceed with caution.
8. (Optional) You can click the task ID to enter the task details page, and then view migration task details and the migration object list.

