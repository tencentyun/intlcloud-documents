TDSQL-C for MySQL allows you to grant and modify database account permissions. As the root account has the read/write permissions of all databases in a TDSQL-C for MySQL cluster, you cannot modify the permissions of the root account. You can grant other accounts the read-write or read-only permissions for created databases on the database management page.

## Prerequisites
- You have created an account other than the root account in your TDSQL-C for MySQL cluster as instructed in [Creating Account](https://www.tencentcloud.com/document/product/1098/44612).
- You have created at least one database in your TDSQL-C for MySQL cluster as instructed in [Creating Database](https://intl.cloud.tencent.com/document/product/1098/44606).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the **Database Management** tab and click **Modify** in the **Operation** column of the target database.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QgpI673_41.png)
3. In the pop-up window, modify the permissions of the account and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GsUX552_42.png)
>?For more information on account authorization, see [Creating Database](https://intl.cloud.tencent.com/document/product/1098/44606#ZHQXSQMX).

