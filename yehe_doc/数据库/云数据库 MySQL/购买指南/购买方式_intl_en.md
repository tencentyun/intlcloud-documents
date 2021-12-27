## Prerequisites
To purchase instances, you need to verify your identity first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing Instances in the Console
1. Log in to the [TencentDB for MySQL purchase page](https://buy.Intl.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region that you want your TencentDB for MySQL instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Database Version**: currently, TencentDB for MySQL supports MySQL 8.0, 5.7, 5.6, and 5.5. For more information on the features of each version, see [official documentation](https://dev.mysql.com/doc/refman/5.7/en/).
  - **Architecture**: single-node, two-node, or three-node. For more information, see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode**: async, semi-sync, and strong sync replication modes are supported. For more information, see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ** and **Replica AZ**: select different source and replica AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
>?
>- If the source and replica nodes are in different AZs, there may be an additional network sync delay of 2–3 ms.
>- When you purchase Tencent Cloud services, we recommend you select the region closest to you to minimize access latency and improve download speed.
 - **Instance Type**: general or dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specs**: select specifications as needed.
 - **Hard Disk**: the disk space is used to store the files required by MySQL execution.
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend that you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Security Group**: for more information on security group creation and management, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 must be opened for the MySQL instance through the inbound rule of the security group. The MySQL instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Parameter Template**: besides the system parameter template provided by TencentDB, you can create a custom parameter template. For more information, see [Managing Parameter Templates](https://intl.cloud.tencent.com/document/product/236/31906).
 - **Alarm Policy**: you can create an alarm policy to trigger alarms and send messages when the Tencent Cloud resource state changes. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project**: select a project to which the TencentDB instance belongs. The default project is used.
 - **Tag**: categorize and manage resources with tags. For more information, see [Tag > Overview](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name**: name the instance now or later.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
 - **Terms of Service**: for more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/236/35543).
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can initialize the instance after around 3-5 minutes when its status changes to **Uninitialized**.

## Purchasing Instances via an API
For more information on how to purchase a TencentDB instance via an API, see [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/236/15865).

## Subsequent Operations
- [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128)
- [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788)

