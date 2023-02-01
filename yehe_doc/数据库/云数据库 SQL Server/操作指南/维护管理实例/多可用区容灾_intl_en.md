## Multi-AZ Deployment
Multi-AZ deployment protects your database against database instance failures and AZ outages. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520).
In TencentDB for SQL Server, multiple AZs are combined into a single multi-AZ to ensure high availability and failover capability of database instances.

#### Failover
TencentDB for SQL Server will handle failover automatically, so you can quickly restore the database operations without administrative intervention. If any of the following conditions occurs, the primary database instance will automatically switch to the replica in the replica AZ.
- AZ outages.
- Primary database instance failure.

>?
>- No matter whether the cluster instances are deployed in multiple AZs, each TencentDB for SQL Server instance has a replica server that supports real-time hot backup to ensure the high availability of the database.
>- In multi-AZ deployment, TencentDB for SQL Server will automatically preset and maintain a synced replica in different AZs.
>- The primary database instance will be synchronously replicated across AZs to the replica to provide data redundancy, eliminate I/O freezes, and minimize latency peak during the system backup.

### Supported regions
TencentDB for SQL Server multi-AZ deployment is supported in Shanghai, Beijing, Guangzhou, and Hong Kong.

### Purchasing a multi-AZ instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click **Create Instance** in the instance list to enter the purchase page.
2. On the TencentDB for SQL Server purchase page, select a supported region, and select a desired replica AZ in the **Multi-AZ** option.
>? Only certain AZs can be selected as a replica AZ. For more information, see the purchase page.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dn7e013_tapd_20397132_base64_1671590124_61.png)
3. Confirm the information you enter, click **Buy Now**. After the purchase is completed, you can return to the instance list to view the newly purchased multi-AZ instance.

## Upgrading to Multi-AZ
You can upgrade disaster recovery capability from single-AZ to multi-AZ for the TencentDB for SQL Server instances in Shanghai, Beijing, and Guangzhou.
>? Upgrading from single-AZ to multi-AZ is free of charge.

1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, select the desired instance, and click **Adjust Configurations** to enter the adjustment page.
2. Select a replica AZ in the **Multi-AZ Deployment** option on the configuration adjustment page.
>?
>- You can’t adjust the multi-AZ configuration when using the publish/subscribe service.
>- As the resources are limited in multi-AZ, you may fail to purchase the resources, and you can [contact us](https://cloud.tencent.com/online-service?from=connect-us) for assistance.
>- Upgrading to multi-AZ deployment will involve instance migration without affecting the normal use. A switch will be performed after migration is completed, which causes a momentary disconnection for few seconds.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/m7r9963_tapd_20397132_base64_1671590296_11.png)
3. Click **OK**. Upgrading to a multi-AZ can be completed when the instance is purchased.

## Relevant Documentation
To migrate the instance to another AZ in the same region, see [Migrating Across AZs] (https://intl.cloud.tencent.com/document/product/238/42695).
