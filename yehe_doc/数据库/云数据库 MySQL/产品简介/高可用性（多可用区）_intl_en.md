Multi-AZ deployment protects your database against database instance failures and AZ outages. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/236/8458).

In TencentDB for MySQL, multiple AZs are combined into a single multi-AZ to ensure high availability and failover capability of database instances.

>?
>- No matter whether the TencentDB for MySQL instances in a database cluster are running across multiple AZs or not, each instance has a replica for real-time hot backup to ensure high database availability.
>- With multi-AZ deployment, TencentDB for MySQL automatically presets and maintains a sync replica in a different AZ.
>- The source database instance is synchronously replicated to the replica across AZs to provide data redundancy, eliminate I/O freezes, and minimize latency during system backups.

### Supported Regions
The multi-AZ deployment scheme of TencentDB for MySQL is currently available in Guangzhou, Shanghai, Beijing, Chengdu, and Virginia regions.

### Multi-AZ Deployment
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/) and click **Create** in the Instance List to enter the purchase page.
2. On the TencentDB for MySQL purchase page, select a supported region, and select a desired replica AZ in the **Replica AZ** option.
>?Only certain AZs can be selected as a replica AZ. For more information, please see the purchase page.
>
![](https://main.qcloudimg.com/raw/d6b71d73ff799a98ba8eb12077269f96.png)
3. After confirming that everything is correct, click **Buy Now**. After making the payment, you can return to the instance list to view the newly purchased multi-AZ instance.

### Failover
TencentDB for MySQL processes failover automatically, so database operations can be resumed as quickly as possible with no administrative intervention required. The source database instance will automatically switch to the replica in the replica AZ in the following conditions:
- AZ outage
-Source database instance failure
