Multi-AZ deployment protects your database from being affected by database instance failures and AZ outages. For more information, please see [Regions and AZs](https://intl.cloud.tencent.com/document/product/236/8458).
The multi-AZ deployment scheme of TencentDB for MySQL guarantees the high availability and failover capability of database instances by combining multiple AZs into a single "multi-AZ".

>?
>- No matter whether the TencentDB for MySQL instances in a database cluster are running across multiple AZs or not, each instance has a slave for real-time hot backup to ensure high database availability.
>- With multi-AZ deployment, TencentDB for MySQL automatically presets and maintains a sync slave replica in a different AZ.
>- The master database instance is synchronously replicated to the slave replica across AZs to provide data redundancy, eliminate I/O freezes, and minimize latency during system backups.

### Supported Regions
The multi-AZ deployment scheme of TencentDB for MySQL is currently available in Guangzhou, Shanghai, Beijing, Chengdu, and Virginia regions.

### Multi-AZ Deployment
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/) and click **Create** in the Instance List to enter the purchase page.
2. On the TencentDB for MySQL purchase page, select a supported region, and select a desired slave AZ in the **Slave AZ** option.
>?Only certain AZs can be selected as a slave AZ. For more information, please see the purchase page.
>
![](https://main.qcloudimg.com/raw/aec9d1b540ceff3426968c213cfe9435.png)
3. After confirming that everything is correct, click **Buy Now**. After making the payment, you can return to the instance list to view the newly purchased multi-AZ instance.

### Failover
TencentDB for MySQL processes failover automatically, so database operations can be resumed as quickly as possible with no administrative intervention required. The master database instance will automatically switch to the slave replica in the slave AZ in the following conditions:
- AZ outage.
- Master database instance failure.
