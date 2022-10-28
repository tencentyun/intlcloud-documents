
This document describes how to create a TencentDB for MySQL instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 380px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>

- To verify your identity:
<div style="background-color:#00A4FF; width: 380px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Purchasing a two-node/three-node instance
1. Log in to the [TencentDB for MySQL purchase page](https://buy.intl.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: Monthly subscription and pay-as-you-go billing are supported.
    - If your business has a stable long-term demand, we recommend you select monthly subscription.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: Select the region where you want to deploy your TencentDB for MySQL instance. We recommend you use the same region as the CVM instance to be connected to. Tencent Cloud services in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Database Version**: Currently, TencentDB for MySQL supports MySQL 8.0, 5.7, 5.6, and 5.5. For more information on the features of each version, see [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/).
 - **Engine**: Select InnoDB or RocksDB.
    - InnoDB: The most commonly used OLTP storage engine, with complete transaction support and powerful capability of highly concurrent reads/writes.
    - RocksDB: A key-value storage engine, with efficient writing and high compression. If it is selected, the architecture will be two-node.
  - **Architecture**: Single-node, two-node, or three-node. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode**: Async, semi-sync, and strong sync replication modes are supported. For more information, see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ** and **Replica AZ**: Select different source and replica AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
>?
>- If the source and replica are in different AZs, the network sync delay may increase by 2–3 ms.
>- When you purchase Tencent Cloud services, we recommend you select the region closest to your end users to minimize access latency and improve download speed.
>
 - **Instance Type**: **General** or **Dedicated**. For more information, see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specs**: Select specifications as needed.
 - **Hard Disk**: The disk space is used to store the files required by MySQL execution.
 - **Network**: Select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Custom Port**: The database access port, which is 3306 by default.
 - **Security Group**: For more information on security group creation and management, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 must be opened for the TencentDB for MySQL instance through the inbound rule of the security group. The instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Parameter Template**: In addition to the system parameter template provided by TencentDB, you can also create a custom parameter template. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
  - **Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After purchasing the instance, you can change the character set on the instance details page in the console. For more information, see [Use Limits > Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity**: Whether the table name is case sensitive. The default value is **Enabled**.
 - **Password Complexity**: You can set the password complexity to improve the database security, which is disabled by default. For more information, see [Setting Password Complexity](https://www.tencentcloud.com/document/product/236/49197).
 - **Root Password**: Set the password of the root account (the default user name for a new MySQL database is "root"). If you select **Set After Creation**, you can reset the password after creating the instance. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
 - **Alarm Policy**: You can create an alarm policy to trigger alarms and send messages when the Tencent Cloud resource state changes. For more information, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project**: Select a project to which the TencentDB instance belongs. The default project is used.
 - **Tag**: Categorize and manage resources with tags. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name**: Name the instance now or later.
 - **Quantity**: You can purchase up to ten pay-as-you-go instances in each AZ.
 - **Purchase Period**: Select the desired duration according to your business needs. The billing mode is monthly subscription, and the longer the purchase period, the higher the discount.
 - **Auto-Renewal**: Auto-renew the device monthly upon expiration if your account has sufficient balance in the monthly subscription billing mode.
 - **Terms of Service**: For more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/236/35543).
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can use the instance after around 3–5 minutes when its status changes to **Running**.

## Purchasing a single-node instance
>?The single-node architecture of the cloud disk edition is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
1. Log in to the [TencentDB for MySQL purchase page](https://buy.intl.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: Monthly subscription and pay-as-you-go billing are supported.
    - If your business has a stable long-term demand, we recommend you select monthly subscription.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: Select the region where you want to deploy your TencentDB for MySQL instance. This architecture is currently supported in Shanghai region and will be available in more regions in the future. We recommend you use the same region as the CVM instance to be connected to. Tencent Cloud services in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Database Version**: Currently, TencentDB for MySQL supports MySQL 8.0 and 5.7 for the single-node architecture. For more information on the features of each version, see [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/).
 - **Engine**: The default engine is InnoDB, which is the most commonly used OLTP storage engine, with complete transaction support and powerful capability of highly concurrent reads/writes.
 - **Architecture**: Select **Single-node**.
 >!As it takes a long time for the basic edition instances to recover, we recommend you use the two-node or three-node version for production environments, which ensures up to 99.99% availability.
 - **Disk Type**: Cloud disk. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).
 - **AZ**: Select an AZ for instance deployment. Tencent Cloud services in different AZs in the same VPC can communicate with each other over the private network; for example, a CVM instance in Shanghai Zone 2 can access a MySQL instance in Shanghai Zone 3 in the same VPC over the private network.
 - **Instance Specs**: Select specifications as needed.
 - **Disk**: The disk space is used to store the files required by MySQL execution. You can select **SSD Cloud Disk** or **Enhanced SSD**. The supported disk capacity range is 20–32000 GB. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).
>?Next configuration steps are the same as those for purchasing two-node/three-node instances. For more information, see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160).
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can use the instance after around 3–5 minutes when its status changes to **Running**.

## Subsequent operations
You can access the TencentDB for MySQL instance over both private and public networks from a Windows or Linux CVM instance. For more information, see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).
