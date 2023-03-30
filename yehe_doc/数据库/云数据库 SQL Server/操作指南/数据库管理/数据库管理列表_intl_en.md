This document describes the fields in the database list.

## Prerequisites
You have created a TencentDB for SQL Server instance. For more information, see [Creating TencentDB for SQL Server Instance](https://www.tencentcloud.com/document/product/238/31571).

## Viewing the database list
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, click **Manage** in the **Operation** column of the target instance to enter the **Instance Details** page.
3. Click **Database Management** to enter the **Database Management** tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qnh5780_20.png)

## Tools
| Tool | Description |
|---------|---------|
| Search box | Click ![](https://qcloudimg.tencent-cloud.cn/raw/4e9962a6b05796851af7e63f3bea18dc.png) to filter databases. You can fuzzy search for databases by database name. |
| Refresh | Click ![](https://qcloudimg.tencent-cloud.cn/raw/309481e9077b12e66da812127caa683a.png) to refresh the list. |

## Fields in the database list

| Field | Description |
|---------|---------|
| Database Name | The name of the database created in the instance. |
| Status | The status of the database. |
| Character Set | The character set information of the database. |
| Database Creation Time | The time when the database was created, which can be sorted in ascending or descending order. |
| Bound Accounts | The accounts authorized to access the database. |
| Description | The description of the database. |
| Operation | <li>Set Permissions: Set the read/write, read-only, or owner permission of the database for an account. <li>Delete: Delete the database. <li>Clone: Quickly clone an existing database to the current instance. <li>Others: Enable/Disable CDC, enable/disable CT, or shrink the database. |

>?For each operation in the database list, you can select multiple databases and click the corresponding batch operation button above the list for batch management.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/3R93632_24.png)

## More
- [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780)
- [Setting Database Permissions](https://intl.cloud.tencent.com/document/product/238/47425)
- [Cloning Database](https://intl.cloud.tencent.com/document/product/238/47426)
- [Deleting Database](https://intl.cloud.tencent.com/document/product/238/35781)
- [Setting Change Data Capture (CDC)](https://intl.cloud.tencent.com/document/product/238/41608)
- [Setting Change Tracking (CT)](https://intl.cloud.tencent.com/document/product/238/41607)
- [Shrinking Database](https://intl.cloud.tencent.com/document/product/238/41606)

