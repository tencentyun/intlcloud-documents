
This document describes how to create a TencentDB for MySQL instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to [MySQL purchase page](https://buy.cloud.tencent.com/cdb), specify the instance information based on your needs and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go billing is supported.
    - If the request volume of your business may fluctuate greatly and instantaneously, we recommend that you choose pay-as-you-go billing.
 - **Region**: select the region where your TencentDB for MySQL instance is deployed. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. Region cannot be modified after purchase.
 - **Primary AZ and Secondary AZ**: select different primary and secondary AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
 >?If the source and replica instances are in different AZs, there may be an additional network sync delay of 2–3 ms.
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend that you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Security Group**: for more information on security group creation and management, please see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).
 >?Port 3306 must be opened for the MySQL instance through the inbound rule of the security group. MySQL instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Architecture**: provide Basic Edition, High-Availability Edition, and Finance Edition. For more information, please see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/17136).
 - **Specify Project**: select a project to which the TencentDB instance belongs. The default project is used by default.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
2. You will be returned to the instance list after purchase. The instance is in the "Delivering" status. You can initialize the instance after around 5-10 minutes and when the status is changed to "Uninitialized".


## Next Steps
For more information on how to initialize a MySQL instance in the console, please see [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128).

