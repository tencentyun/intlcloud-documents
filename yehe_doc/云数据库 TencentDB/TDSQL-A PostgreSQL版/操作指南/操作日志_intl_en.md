This document describes how to view the slow log and error log details of a TDSQL-A for PostgreSQL instance in the console.

## Slow Log Details
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Operation Log** tab, click **Slow Log Details**, select a time to view the slow log information.
![](https://main.qcloudimg.com/raw/1bc495cf724108d9cc0ee6e01ad69878.png)
 - You can query slow log information by time.
 ![](https://main.qcloudimg.com/raw/e5376762d6b2431af50692f8a72db504.png)
 - You can also search by database name.
 ![](https://main.qcloudimg.com/raw/97b7abee37cec982f100e8b56a81bd33.png)
 
## Error Log Details
Error information in the operation logs generated during database operation is recorded in error log details.

1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Operation Log** tab, click **Error Log Details**, and select a time to view the error log information.
 ![](https://main.qcloudimg.com/raw/7b4b07d7ad27a3f49f5d7e93b5c7eeac.png)

