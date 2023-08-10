This document describes how to set up a 2-region-3-DC architecture by deploying instances across AZs and creating a remote disaster recovery instance.

## 2-Region-3-DC Deployment Architecture
![](https://qcloudimg.tencent-cloud.cn/raw/1ad2c4f70918774892a6b453c80d3186.png)
- 1-region-2-DC:
Zones 3 and 5 in region A form a 1-region-2-DC architecture. If zone 3 fails, you can switch to zone 5 to protect the database.
- Cross-region disaster recovery:
Regions A and B form a cross-region disaster recovery architecture. Even if all data centers in zones 3 and 5 in region A fail, the business can continue after being switched to a data center in region B.

## Multi-AZ Deployment
TencentDB for MySQL supports multi-AZ deployment. Compared with a single-AZ deployment scheme, a multi-AZ one has better disaster recovery capabilities and can protect your database from being affected by database instance failures, AZ outages, and even IDC-level failures.

In TencentDB for MySQL, multiple AZs are combined into a single multi-AZ to ensure high availability and failover capability of database instances.
![](https://qcloudimg.tencent-cloud.cn/raw/d36cb036272104a4be5e763ce38a82e2.png)

### Prerequisites
- The instance is running.
- The region where your instance resides should have at least two AZs.
- The target AZs have sufficient computing resources.

### Supported regions and AZs
Currently, multi-AZ deployment of TencentDB for MySQL is supported in Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Hong Kong (China), Singapore, Jakarta, Bangkok, Mumbai, Seoul, Tokyo, Virginia, and Frankfurt regions. Available source and replica AZs in different regions are as displayed on the [TencentDB for MySQL purchase page](https://buy.Intl.cloud.tencent.com/cdb).
- This feature will gradually support more regions and AZs.
- If you want to deploy an instance in other regions or AZs to meet your business needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### Billing description
This feature is free of charge. There is no charge for migrating an instance from a single AZ to multiple AZs.

## Cross-Region Disaster Recovery Instance
For applications with high requirements of service continuity, data reliability, and compliance, TencentDB for MySQL provides cross-region disaster recovery instances to help enhance your capability to deliver continued services at low costs and improve data reliability.
With a separate database connection address, a cross-region disaster recovery instance can offer read access capability for various scenarios such as nearby access and data analysis at a lower cost of device redundancy. Its highly available source/replica architecture helps avoid single points of failure for databases.
![](https://qcloudimg.tencent-cloud.cn/raw/bf639c6f2d80718b2c272cfc0008be54.png)

### Billing description
A disaster recovery instance costs the same as the source instance associated with it.

## Setting up 2-Region-3-DC Architecture
### Step 1. Set multi-AZ deployment
#### Selecting multi-AZ deployment during instance purchase
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/) and click **Create** in the instance list to enter the purchase page.
2. On the purchase page, select a supported region and then select an AZ different from the source AZ for **Replica AZ**.
>?If the source and replica are in different AZs, the network sync delay may increase by 2–3 ms.
>
![](https://qcloudimg.tencent-cloud.cn/raw/1713bdbe69eae9890560c36283cd52ef.png)
3. After confirming that everything is correct, click **Buy Now**. After making the payment, you can view the instance's source and replica AZs in **Availability Info** on the **Instance Details** page.

#### Changing single-AZ deployment to multi-AZ deployment for existing instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, click the ID or **Manage** in the **Operation** column of the target instance to enter the **Instance Details** page.
3. In **Availability Info** > **Deployment Mode** on the **Instance Details** page, click **Modify Replica AZ**.
![](https://qcloudimg.tencent-cloud.cn/raw/c0e598dbb2c9459397f62f155b2d7413.png)
4. In the pop-up window, select **Yes** for **Multi-AZ Deployment**, select a replica AZ, and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/8730f424e5a67407cc6f966d774f92cf.png)

### Step 2. Set a cross-region disaster recovery instance
>?Disaster recovery instances can be purchased only for high available GTID-enabled source instances on MySQL 5.6 or later with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or later. If your source instance is below this specification, upgrade it first.

#### 2.1 Create a disaster recovery instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the details page.
2. Make sure that the GTID feature is enabled by viewing the basic information of the instance on the **Instance Details** page. Click **Add Disaster Recovery Instance** in the instance architecture diagram to enter the disaster recovery instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/45177bca4dd63114c97eee5a45ab72b9.png)
3. On the purchase page, configure the basic information of the disaster recovery instance, such as **Billing Mode**, **Region**, and **Sync Policy**.
 - If the sync policy is **Sync Now**, data will be synced immediately when the disaster recovery instance is created.
 - If the sync policy is **Sync After Creation**, you need to configure a disaster recovery sync link after the instance is created successfully. For detailed directions, see [Create a sync link](#cjtblj) below.
>?
>- The time required to complete the creation depends on the amount of data, and no operations can be performed on the source instance in the console during the creation. We recommend you do so at an appropriate time.
>- Only the entire instance data can be synced. Make sure that the disk space is sufficient.
>- You need to ensure that the source instance is in the running state and none of configuration adjustment tasks, restart tasks, and other modification tasks are executed. Otherwise, the sync task may fail.  
4. After confirming that everything is correct, click **Buy Now** and wait for disaster recovery instance delivery.
5. Return to the instance list. After the status of the instance changes to **Running**, it can be used normally.

## Viewing 2-Region-3-DC Architecture
After the configuration is completed, the database is deployed in 2-region-3-DC architecture as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4e541bac303a064366b980080d6178aa.png)
