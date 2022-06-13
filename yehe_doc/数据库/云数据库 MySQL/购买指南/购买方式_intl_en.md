## Prerequisites
To make a purchase, you need to complete identity verification first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing in Console
1. Log in to the [TencentDB for MySQL purchase page](https://buy.intl.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: Monthly subscription and pay-as-you-go billing are supported.
    - If your business has a stable long-term demand, we recommend you select monthly subscription.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: Select the region where you want to deploy your TencentDB for MySQL instance. We recommend you use the same region as the CVM instance to be connected to. Tencent Cloud services in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Database Version**: Currently, TencentDB for MySQL supports MySQL 8.0, 5.7, 5.6, and 5.5. For more information on the features of each version, see the [official documentation](https://dev.mysql.com/doc/refman/5.7/en/).
 - **Engine**: Select InnoDB or RocksDB.
    - InnoDB: The most commonly used OLTP storage engine, with complete transaction support and powerful capability of highly concurrent reads/writes.
    - RocksDB: A key-value storage engine, with efficient writing and high compression. If it is selected, the architecture will be two-node.
  - **Architecture**: Single-node, two-node, or three-node. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode**: Async, semi-sync, and strong sync replication modes are supported. For more information, see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ** and **Replica AZ**: Select different source and replica AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
>?
>- If the source and replica are in different AZs, the network sync delay may increase by 2–3 ms.
>- When purchasing Tencent Cloud services, we recommend you choose the region closest to your end users to reduce access latency and improve download speed.
>
 - **Instance Type**: General or dedicated. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specification**: Select specifications as needed.
 - **Hard Disk**: The disk space is used to store the files required by MySQL execution.
 - **Network**: Select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Custom Port**: The database access port, which is 3306 by default.
 - **Security Group**: For more information on security group creation and management, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 must be opened for the TencentDB for MySQL instance through the inbound rule of the security group. The instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Parameter Template**: Besides the system parameter template provided by TencentDB, you can create a custom parameter template. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
  - **Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After purchasing the instance, you can change the character set on the instance details page in the console. For more information, see [Use Limits > Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity**: Whether the table name is case sensitive. The default value is **Enabled**.
 - **Root Password**: Set the password of the root account (the default user name for a new MySQL database is "root"). If you select **Set After Creation**, you can [reset the password](https://intl.cloud.tencent.com/document/product/236/31901) after creating the instance.
 - **Alarm Policy**: You can create an alarm policy to trigger alarms and send messages when the Tencent Cloud resource state changes. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project**: Select a project to which the TencentDB instance belongs. The default project is used.
 - **Tag**: Categorize and manage resources with tags. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name**: Name the instance now or later.
 - **Quantity**: You can purchase up to 10 pay-as-you-go instances in each AZ.
 - **Purchase Period**: Select the desired duration according to your business needs. The billing mode is monthly subscription, and the longer the purchase period, the higher the discount.
 - **Auto-Renewal**: Auto-renew the device monthly upon expiration if your account has sufficient balance in the monthly subscription billing mode.
 - **Terms of Service**: For more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/236/35543).
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can use the instance after around 3–5 minutes when its status changes to **Running**.

## Purchasing via API
For more information on how to purchase TencentDB instances via an API, see [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/236/15865).

## Subsequent Operations
[Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788)

