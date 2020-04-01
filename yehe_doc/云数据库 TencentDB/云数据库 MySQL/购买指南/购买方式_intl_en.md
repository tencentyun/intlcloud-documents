## Prerequisites
To make a purchase, you need to verify your identity first. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing at Official Website
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and click **Create** in the instance list to enter the purchase page.
 ![](https://main.qcloudimg.com/raw/8440c63d34e0cdbfec26348ee37f1f17.png)
2. Select various configuration items on the purchase page based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: only pay-as-you-go billing is supported.
    - If the request volume of your business may fluctuate greatly and instantaneously, you are recommended to choose pay-as-you-go billing.
 - **Region**: select the region where the TencentDB for MySQL instance is deployed for your business. Tencent Cloud products in different regions cannot communicate with each other over the private network. This parameter cannot be modified after purchase.
 - **Master and Slave AZs**: you are recommended to deploy the master and slave in the same AZ so as to avoid network delay issues.
 - **Network**: select the network where TencentDB for MySQL instance resides, which is "Default-VPC (Default)" by default.
 - **Security Group**: for more information on security group creation and management, please see [TencentDB Security Groups](https://intl.cloud.tencent.com/document/product/236/14470).
 - **Architecture**: basic and high-availability editions are available.
 - **Project**: select a project to which the database instance belongs. The default project is used by default.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
 
## Purchasing Through API
For more information on how to purchase a TencentDB instance through the API, please see [Creating Instances](https://intl.cloud.tencent.com/document/product/236/15871).
