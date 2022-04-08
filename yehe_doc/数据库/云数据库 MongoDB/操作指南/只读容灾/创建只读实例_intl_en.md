TencentDB for MongoDB allows to you create and manage read-only instances in the console.

## Background
TencentDB for MongoDB allows you to create one or more read-only instances. They are suitable for read/write separation and capable of reducing the request pressure on the primary instance and enhancing the read load capacity of your business
>? 
>- The sync latency between the read-only instances and the primary instance can be viewed in the console.
>- Due to the delay in data sync, the real-timeness of data sync for read-only instances may not be guaranteed. If your business requires read/write separation and high real-timeness, we recommend your business read the secondary nodes of the primary instance. For more information, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).
>- Read-only instances are connected in the same way as the primary instance. For more information, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).
>- During its lifecycle, a read-only instance can be read only but not written.
>- When a read-only instance is disconnected from the primary instance during sync or is promoted to the primary instance manually in the console, it will become a general instance that can be normally read/written.

## Infrastructure 
Changes on the primary instance are synced to read-only instances through oplog. Each read-only instance adopts an architecture of at least one primary instance and two secondary instances as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0e3cf94b27a79e4eec31602c8e9fe3f9.svg)

## Version Requirement
Currently, only TencentDB for MongoDB 3.2, 3.6, and 4.0 instances support read-only instance creation.

## Use Limits 
- Up to three read-only instances can be created for a primary instance.
- The engine of a read-only instance must be the same as that of the primary instance.
- Backup and rollback: Backup and rollback are not supported.
- Data migration: Migrating data to read-only instances is not supported.
- Database management: Database creation and deletion are not supported.
- Account management: Account creation/deletion, password reset, and account authorization are not supported.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The instance is running normally.

## Directions
### Viewing read-only instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/sharding).
2. On the left sidebar, select **NoSQL** > **MongoDB**.
3. In the **MongoDB** drop-down list, select **Replica Set Instance** or **Sharded Cluster Instance**. The operation steps for both instance types are similar.
4. Above the instance list on the right, select the region.
5. In the instance list, find the target instance.
6. Click the target instance ID to enter the **Instance Details** page.
7. Select the **RO/DR** > **Read-Only Instance** tab.
8. View the new read-only instances under the current instance.

### Creating read-only instance
1. On the **Read-Only Instance** tab, click **Create**.
2. On the **TencentDB for MongoDB Read-Only Instance** purchase page, confirm the **primary instance information** and select the required configuration.
3. Click **Buy Now**. After the purchase, you can return to the **Read-Only Instance** tab to manage read-only instances.
![](https://qcloudimg.tencent-cloud.cn/raw/a43d7075f2bc144a9eba9a988c4f0f59.png)

### Adjusting read-only instance configuration
1. On the **Read-Only Instance** tab, find the target read-only instance.
2. In the **Operation** column, click **Adjust Configuration**.
3. On the **Adjust Configuration** page, you can adjust the node specification, node capacity, and oplog capacity.
4. In the **Switch Time** option, select the specific time for instance specification switch.
   - If you select **Upon modification completion**, the instance specification adjustment task will be executed immediately.
   - If you select **Maintenance time**, the instance specification switch task will be executed during the maintenance time.
> ! We recommend you set the **maintenance time** to be within off-peak hours of your business, and you need to regularly maintain your instance. If you select **Upon modification completion**, the instance configuration will be adjusted immediately, which may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, we strongly recommend you make the instance configuration executed within the **maintenance time**. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/240/31190).
5. You can click **Billing Details** to view billable items and billing formula and confirm the **fees**.
6. After confirming that everything is correct, click **Submit**.

### Renewing read-only instance
1. On the **Read-Only Instance** tab, find the target read-only instance.
2. Click **Renew** above the instance list and select the renewal period in the **Renew Selected Instance** window.
3. Confirm the total renewal fees and click **OK**.

### Setting auto-renewal
1. On the **Read-Only Instance** tab, find the target read-only instance.
2. Click **Set Auto-Renewal** above the instance list and confirm the auto-renewal item and renewal expiration time in the **Set Auto-Renewal** window.
3. Confirm the total renewal fees and click **OK**.

### Disabling auto-renewal
1. On the **Read-Only Instance** tab, find the target read-only instance.
2. Click **Disable Auto-Renewal** above the instance list and confirm the instance information.
3. Click **OK**.

## Related APIs
| API              | Description                                                      |
| ------------------- | ------------------------------------------------------------ |
| DescribeDBInstances | [Queries TencentDB instance list](https://intl.cloud.tencent.com/document/product/240/34702) |
| RenameInstance       | [Renames instance](https://intl.cloud.tencent.com/document/product/240/34697) |
| RenewDBInstances     | [Renews TencentDB instance](https://intl.cloud.tencent.com/document/product/240/37326) |

