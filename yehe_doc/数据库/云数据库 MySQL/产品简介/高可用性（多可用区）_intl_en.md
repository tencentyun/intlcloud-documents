
Multi-AZ deployment protects your database against database instance failures and AZ outages. For more information on supported regions and AZs, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/236/8458).
In TencentDB for MySQL, multiple AZs are combined to form a single multi-AZ architecture to ensure high availability and failover capability of database instances.

>?
- No matter whether the cluster instances are deployed in multiple AZs, each TencentDB for MySQL instance has a replica server that supports real-time hot backup to ensure the high availability of the database.
- In multi-AZ deployment, TencentDB for MySQL will automatically preset and maintain a synced replica in different AZs.
- The source database instance will be synchronously replicated across AZs to the replica to provide data redundancy, eliminate I/O freezes, and minimize latency peak during the system backup.

### Supported regions
Currently, the multi-AZ deployment of TencentDB for MySQL is supported in Guangzhou, Shenzhen Finance, Shanghai, Shanghai Finance, Nanjing, Beijing, Chengdu, Hong Kong (China), Singapore, Jakarta, Bangkok, Mumbai, Seoul, Tokyo, Virginia, and Frankfurt regions.

### Multi-AZ deployment
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/) and click **Create** in the **Instance List** to enter the purchase page.
2. On the TencentDB for MySQL purchase page, select a supported region, and select a desired replica AZ in the **Multi-AZ** option.
>? Only certain AZs can be selected as a replica AZ. For more information, see the purchase page.
>
![](https://main.qcloudimg.com/raw/d6b71d73ff799a98ba8eb12077269f96.png)
3. Confirm the information you enter and click **Buy Now**. After the purchase is completed, you can return to the instance list to view the newly purchased multi-AZ instance.

### Failover
TencentDB for MySQL will handle failover automatically, so you can quickly restore the database operations without administrative intervention. If any of the following conditions occurs, the source database instance will automatically switch to the replica in the replica AZ.
- AZ outages.
- Source database instance failure.
