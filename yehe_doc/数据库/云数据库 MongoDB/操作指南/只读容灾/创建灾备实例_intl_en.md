TencentDB for MongoDB allows to you create and manage disaster recovery instances in the console.

## Background
TencentDB for MongoDB allows you to create one or more disaster recovery instances. For applications with high requirements of service continuity, data reliability, and compliance, such instances help enhance your capability to deliver continued services at low costs and improve data reliability.
>?
>- Due to the delay in data sync, the real-timeness of data sync for disaster recovery instances may not be guaranteed. Sync latency between the disaster recovery instances and the primary instance can be viewed in the console.
>- A disaster recovery instance can only be read but not written during its lifecycle.
>- When a disaster recovery instance is disconnected from the primary instance during sync or is promoted to the primary instance manually in the console, it will become a general instance that can be normally read/written.


## Version Requirement
Currently, only TencentDB for MongoDB 3.2, 3.6, and 4.0 instances support disaster recovery instance creation.

## Use Limits 
- Up to three disaster recovery instances can be created for a primary instance.
- Backup and rollback: They are not supported.
- Data migration: Migrating data to disaster recovery instances is not supported.
- Database management: Database creation and deletion are not supported.
- Account management: Account creation/deletion, password reset, and account authorization are not supported.
- The engine of a disaster recovery instance must be the same as that of the primary instance.
- Due to network isolation, you cannot create disaster recovery instances in finance zones for primary instances in general regions, and vice visa.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The replica set instance is running normally.

## Directions 
You can view, create, and renew disaster recovery instances, adjust their configurations, and set auto-renewal for them in the console.

### Viewing disaster recovery instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/sharding).
2. On the left sidebar, select **NoSQL** > **MongoDB**.
3. In the **MongoDB** drop-down list, select **Replica Set Instance** or **Sharded Cluster Instance**. The operation steps for both instance types are similar.
4. Above the instance list on the right, select the region.
5. In the instance list, find the target instance.
6. Click the target instance ID to enter the **Instance Details** page.
7. Select the **RO/DR** > **DR Instance** tab.
8. View the new disaster recovery instances under the current instance.

### Creating disaster recovery instance
1. On the **DR Instance** tab, click **Create**.
2. On the **TencentDB for MongoDB DR Instance** purchase page, confirm the **primary instance information** and select the required configuration.
3. Click **Buy Now**. After the purchase, you can return to the **DR Instance** tab to manage disaster recovery instances.
![](https://qcloudimg.tencent-cloud.cn/raw/f869ce9e0503a54e9db81024ce789db6.png)

### Adjusting disaster recovery instance configuration
1. On the **DR Instance** tab, find the target disaster recovery instance.
2. In the **Operation** column, click **Adjust Configuration**.
3. On the **Adjust Configuration** page, you can adjust the node specification, node capacity, and oplog capacity.
4. In the **Switch Time** option, select the specific time for instance specification switch.
   - If you select **Upon modification completion**, the instance specification adjustment task will be executed immediately.
   - If you select **Maintenance time**, the instance specification switch task will be executed during the maintenance time.
> ! We recommend you set the **maintenance time** to be within off-peak hours of your business, and you need to regularly maintain your instance. If you select **Upon modification completion**, the instance configuration will be adjusted immediately, which may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, we strongly recommend you make the instance configuration executed within the **maintenance time**. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/240/31190).
5. You can click **Billing Details** to view billable items and billing formula and confirm the **fees**.
6. After confirming that everything is correct, click **Submit**.

### Renewing disaster recovery instance
1. On the **DR Instance** tab, find the target disaster recovery instance.
2. Click **Renew** above the instance list and select the renewal period in the **Renew Selected Instance** window.
3. Confirm the total renewal fees and click **OK**.

### Setting auto-renewal
1. On the **DR Instance** tab, find the target disaster recovery instance.
2. Click **Set Auto-Renewal** above the instance list and confirm the auto-renewal item and renewal expiration time in the **Set Auto-Renewal** window.
3. Confirm the total renewal fees and click **OK**.

### Disabling auto-renewal
1. On the **DR Instance** tab, find the target disaster recovery instance.
2. Click **Disable Auto-Renewal** above the instance list and confirm the instance information.
3. Click **OK**.

## Related APIs
| API              | Description                                                      |
| -------------------- | ------------------------------------------------------------ |
| DescribeDBInstances  | [Queries TencentDB instance list](https://intl.cloud.tencent.com/document/product/240/34702) |
| RenameInstance       | [Renames instance](https://intl.cloud.tencent.com/document/product/240/34697) |
| RenewDBInstances     | [Renews TencentDB instance](https://intl.cloud.tencent.com/document/product/240/37326) |
| ModifyDBInstanceSpec | [Adjusts TencentDB instance configuration](https://intl.cloud.tencent.com/document/product/240/34699) |

