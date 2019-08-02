## Use Limitations

1. TencentDB for SQL Server **do not allow the creation/deletion of databases and creatin/deleting/modifying accounts via Microsoft SQL Server Management. If needed, please log in to the Tencent Cloud [Console](https://console.cloud.tencent.com/sqlserver) to do so.
When you try to manage databases in Microsoft SQL Server Management, the system may prompt "An exception occurred while executing a Transact-SQL statement or batch processing".

2. Tencent Cloud **prohibits the sysadmin role**. If your business has to use this role, please contact your Tencent Cloud account manager.
When you try to manage databases in Microsoft SQL Server Management, the system may prompt "You must be a member of the sysadmin role to perform this operation".

3. **The use of SQL Server agent is supported.**







