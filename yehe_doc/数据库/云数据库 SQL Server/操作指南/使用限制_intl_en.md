- Do not use the Microsoft SQL Server Management Studio (SSMS) to create or delete databases, or create, delete, or modify database accounts, or else the message "An exception occurred while executing a Transact-SQL statement or batch processing" may be prompted. You can perform these operations in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).

- For dual-server high availability or cluster instances, TencentDB for SQL Server prohibits the `sysadmin` role by default to avoid the risk of intrusion. If your business has to use this role, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
When you try to manage databases in SSMS, the message "You must be a member of the sysadmin role to perform this operation" may be prompted.

- For basic edition instances, TencentDB for SQL Server allows the admin account to grant a user the permission to use the `sysadmin` role. 
