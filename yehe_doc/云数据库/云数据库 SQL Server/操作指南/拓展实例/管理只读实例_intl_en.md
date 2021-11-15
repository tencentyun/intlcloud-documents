
You can create, view, and terminate read-only instances in the TencentDB for SQL Server console.

>?Read-Only instances cannot be purchased and used separately; instead, they must be bound to a primary instance (Dual-Server High Availability Edition or Cluster Edition).

## Feature Limits
- Up to 3 read-only instances can be created for a primary instance.
- Currently, read-only instances are not supported for Standard Edition.
- Currently, read-only instances cannot be added to instances in finance zones.
- Read-Only instances do not support backup and rollback.
- Data cannot be migrated to read-only instances.
- Read-Only instances do not support database creation/deletion. If needed, please operate on a primary instance.
- Read-Only instances do not support account creation/deletion/authorization and account name/password change. If needed, please operate on a primary instance.


## Creating Read-Only Instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the details page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** on the instance details page or click **Create** on the **Read-Only Instance** page to enter the purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/9f46d9d3fe5a77819b68d9fe1081813f.png)
3. On the purchase page, select the desired read-only instance configuration, confirm that everything is correct, and click **Buy Now**.
>?If you need to unify the expiration time of the primary and read-only instances, you can set the collective expiration date in the [Renewal Management console](https://console.cloud.tencent.com/account/renewal).
>
![](https://qcloudimg.tencent-cloud.cn/raw/407fa77c69d571162dc711299f8d91c8.png)


## Viewing Read-Only Instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, instances with an **R** flag are read-only instances. Click an instance ID or **Manage** in the **Operation** column to enter the read-only instance details page.
2. In the **Instance Architecture Diagram** on the instance details page, you can view the information of the bound primary instance. You can click the instance ID to enter the details page of the primary instance. You can also enter the details page of the read-only instance from the **Instance Architecture Diagram** of the primary instance.
>?Some features on the read-only instance details page cannot be modified and are synced from the primary instance. If you need to change them, please do so on the primary instance details page.
>
![](https://qcloudimg.tencent-cloud.cn/raw/b5f90a8f7c0ad4e1de69af51cbdfd107.png)


## Terminating Read-Only Instance
An read-only instance can be terminated in the same way as a primary instance as instructed in [Terminating Instance](https://intl.cloud.tencent.com/document/product/238/35787).
