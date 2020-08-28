
This document describes how to create a TencentDB for MySQL instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 370px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to register a Tencent Cloud account</a></div>
- To verify your identity:
<div style="background-color:#00A4FF; width: 370px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in and go to the [TencentDB for MySQL purchase page](https://buy.cloud.tencent.com/cdb), select various configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - **Billing mode**:
    - If the request volume of your business may fluctuate greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region where your TencentDB for MySQL instance is deployed. Tencent Cloud services in different regions cannot communicate with each other over the private network. Region cannot be modified after purchase.
 - **Primary AZ and Secondary AZ**: selecting different primary and secondary AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) can protect your database from failures and AZ outages.
 >?If the source and replica are in different AZs, there may be an additional network sync delay of 2–3 ms.
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default.
 - **Security Group**: for more information on security group creation and management, please see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).
 >?Port 3306 must be opened for the TencentDB for MySQL instance through the inbound rule of the security group. The instance uses private network port 3306 by default and supports customizing the port. If the default port is changed, the new port should be opened in the security group.
 - **Architecture**: Basic Edition, High-Availability Edition, and Finance Edition are provided. For more information, please see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/17136).
 - **Specify Project**: select a project to which the database instance belongs. The default project is used by default.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
2. After making the payment, return to the instance list, wait for the instance status to become "uninitialized", and initialize the instance.


## Subsequent Steps
Initialize the TencentDB for MySQL instance in the console as instructed in [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128).


