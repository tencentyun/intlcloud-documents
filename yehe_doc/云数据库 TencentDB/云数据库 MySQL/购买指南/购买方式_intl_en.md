## Prerequisites
To make a purchase, you need to verify your identity first. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing via official website
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and click **Create** in the instance list to enter the purchase page.
 ![](https://main.qcloudimg.com/raw/8440c63d34e0cdbfec26348ee37f1f17.png)
2. Configure items on the purchase page based on your actual needs, confirm the information, and click **Buy Now**.
 - **Billing Mode**: only pay-as-you-go is supported.
 - **Region**: select the region where your TencentDB for MySQL instance is deployed. Tencent Cloud products in different regions cannot communicate with each other over the private network. Region cannot be modified after purchase.
 - **Master AZ and Slave AZ**: select different master and slave AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) can protect your database from failures and AZ outages.
 >If the master and slave are in different AZs, there may be an additional network sync delay of 2–3 ms.
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default.
 - **Security Group**: for more information on security group creation and management, please see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).
 >Port 3306 must be opened for the MySQL instance through the inbound rule of the security group. MySQL instance uses private network port 3306 by default and supports customizing the port. If the default port is changed, the new port should be opened in the security group.
 - **Architecture**: Basic Edition, High-Availability Edition, and Finance Edition are provided. For more information, please see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/17136).
 - **Specify Project**: select a project to which the database instance belongs. The default project is used by default.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
 
## Purchasing via API
For more information on how to purchase a TencentDB instance via API, please see [CreateDBInstance](https://intl.cloud.tencent.com/document/product/236/15865).


## Subsequent Steps
- [Initializing CDB for MySQL](https://intl.cloud.tencent.com/document/product/236/3128)
- [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130)

