## Functional Limitations

**1. Tencent Cloud prohibits the operations to **create and delete databases and create, delete and modify accounts** using Microsoft SQL Server Management. If needed, please log in to the Tencent Cloud [Console](https://console.cloud.tencent.com/sqlserver) to do so.**
When trying to manage databases in Microsoft SQL Server Management, the system may prompt "An exception occurred while executing a Transact-SQL statement or batch".

**2. Tencent Cloud prohibits the sysadmin role. If your business has to use this role, please contact Tencent Cloud staff for a solution.**
When trying to manage databases in Microsoft SQL Server Management, the system may prompt "You must be a member of the sysadmin role to perform this operation".

**3. The use of SQL Server agent is not supported.**







