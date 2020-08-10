## Prerequisites
To make a purchase, you need to verify your identity first. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Purchasing at Official Website
1. Log in at the [purchase page](https://buy.cloud.tencent.com/cdb), select various configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
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

## Purchasing Through API
For more information on how to purchase a TencentDB instance through API, please see [CreateDBInstance](https://intl.cloud.tencent.com/document/product/236/15871).


## Subsequent Steps
- [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128)
- [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3130)

