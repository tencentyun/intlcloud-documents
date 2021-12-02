
This document describes how to create a TencentDB for MySQL instance in the console.

## Prerequisite
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TencentDB for MySQL purchase page](https://Intl.buy.cloud.tencent.com/cdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region that you want your TencentDB for MySQL instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
  - **Architecture**: two-node and three-node. For more information, please see [Database Architecture](https://intl.cloud.tencent.com/document/product/236/38328).
 - **Source AZ** and **Replica AZ**: select different source and replica AZs (i.e., [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/236/8459)) to protect your database from failures and AZ outages.
>?If the source and replica nodes are in different AZs, there may be an additional network sync delay of 2–3 ms.
 - **Resource Isolation Policy**: general or dedicated. For more information, please see [Resource Isolation Policy](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specification**: general or dedicated
    - General: the instance uses the allocated memory and disk resources exclusively and share the CPU resources with other general instances on the same physical machine.
    - Dedicated: the instance uses the allocated CPU, memory, and storage resources exclusively.
 - **Hard Disk**: the disk space is used to store the files required by MySQL execution.
 - **Data Replication Mode**: async, semi-sync, and strong sync replication modes are supported. For more information, please see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Network**: select the network where the TencentDB for MySQL instance resides, which is "Default-VPC (default)" by default. We recommend that you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Security Group**: for more information on security group creation and management, please see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 must be opened for the MySQL instance through the inbound rule of the security group. The MySQL instance uses private network port 3306 by default and supports custom port. If the default port is changed, the new port should be opened in the security group.
 - **Parameter Template**: besides the system parameter template provided by TencentDB, you can create a custom parameter template. For more information, please see [Managing Parameter Templates](https://intl.cloud.tencent.com/document/product/236/31906).
 - **Alarm Policy**: you can create an alarm policy to trigger alarms and send messages when the Tencent Cloud resource state changes. For more information, please see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project**: select a project to which the TencentDB instance belongs. The default project is used.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
 - **Character Set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is UTF8. After initializing the instance, you can change the character set on the instance details page in the console. For more information, see [Use Limits > Notes on character set](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity**: whether the table name is case sensitive. The default value is yes.
 - **Custom Port**: the database access port, which is 3306 by default.
 - **Root Account Password**: set the password of the root account (the default user name for a new MySQL database is "root").
 - **Confirm Password**: enter the password again.
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can operate the instance after around 3-5 minutes when its status changes to **Running**.

## Subsequent Operations
You can access the TencentDB for MySQL instance over both private and public networks from a Windows or Linux CVM instance. For more information, see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).
