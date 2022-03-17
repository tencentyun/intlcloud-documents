This document describes how to modify the primary and standby AZs of an instance in the TencentDB for PostgreSQL console. Modifying AZs has no impact on the instance’s properties, configurations, or connection addresses. The amount of time required to modify AZs depends on the data volume of the instance.

## Background
- Compared with a single-AZ deployment scheme, a multi-AZ one has better disaster recovery capabilities and can protect your database from being affected by database instance failures, AZ outages, and even IDC-level failures.
- The multi-AZ deployment scheme guarantees the high availability and failover capability of database instances by combining multiple AZs in the same region into a single "multi-AZ".

## Notes
- The region where your instance resides should have at least two AZs.
- The target AZ has sufficient computing resources.
- Because a read-only instance has only one node, it cannot use the multi-AZ deployment scheme. The region where the read-only instance resides will not change if the AZs of its primary instance change.

## Costs
There is no additional charge for the time being.

## Directions
### Selecting AZs on the instance purchase page
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and click **Create**.
2. On the displayed purchase page, select a region, **Primary AZ**, and **Standby AZ**.
![](https://qcloudimg.tencent-cloud.cn/raw/55e0b1ab8457aafa68b50d50fe73bcf2.png)
3. After the instance is purchased, you can view its primary and standby AZs in the **Availability Info** block on the **Instance Details** tab.

### Modifying AZs in the console
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, select a region and click an instance ID to access the instance management page.
2. Click **Modify AZ** in the **Availability Info** block on the **Instance Details** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/12af54be79189b30b058bef8b551b7b6.png)
3. In the pop-up **Modify Deployment Info** window, select AZs for the primary node and the standby node, respectively.
>!The default data replication mode is synchronous replication, which prioritizes data integrity. The instance performance is affected by the log transmission efficiency.
4. Select the switch time and click **OK**.
 - Specify time: The switch will occur during the period of time you select.
 - Upon modification completion: The switch will occur right after the modification is completed.
>?Modifying the primary AZ of an instance will trigger an instance switch, during which the database will be temporarily disconnected. Make sure that your business has a reconnection mechanism. However, modifying the standby AZ has no impact on instance access.
>
5. After the instance status changes from **Modifying AZ** to **Running**, the AZ modification is completed.
