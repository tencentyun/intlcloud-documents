This document describes how to create a TDSQL for MySQL instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 370px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To complete identity verification:
<div style="background-color:#00A4FF; width: 370px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TDSQL for MySQL purchase page](https://console.cloud.tencent.com/tdsqld/tdmysql-buy), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: Pay-as-you-go billing is supported.
    - If your business has a stable long-term demand, we recommend you select monthly subscription.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: Select the region where you want to deploy your TDSQL for MySQL instance. We recommend you use the same region as the CVM instance to be connected to. Tencent Cloud services in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Network**: Select the network where the TDSQL for MySQL instance resides. We recommend you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the MySQL instance cannot connect to the CVM instance over the private network.
 - **Instance Version**: For more information, see [Instance Architecture](https://intl.cloud.tencent.com/document/product/1042/33319).
 - **Source AZ** and **Replica AZ**: Select different source and replica AZs to protect your database from failures and AZ outages.
 - **Kernel Version**: The MySQL 5.6 kernel does not support distributed transactions (XA). If you need this feature, select v5.7. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1042/38142).
 - **Shard Quantity/Specification/Disk**: Two, four, or eight shards are recommended to avoid data skew. For more information on shard configuration, see [Selection of TDSQL Instance and Shard Configuration](https://intl.cloud.tencent.com/document/product/1042/33354).
 - **Project**: Select a project to which the instance belongs. The default project is used.
 - **Tag**: Categorize and manage resources with tags. For more information, see [Tag Overview](https://intl.cloud.tencent.com/document/product/651/13334).
 - **Security Group**: For more information on security group creation and management, see [Security Group Configuration](https://intl.cloud.tencent.com/document/product/1042/33348).
 - **Instance Name**: Name the instance now or later.
 - **Supported character sets**: UTF8, LATIN1, GBK, UTF8MB4, and GB18030 are supported.
 - **Table Name Case Sensitivity**: Select **Case sensitive (lower_case_table_names = 0)** or **Case insensitive (lower_case_table_names = 1)**. It is an initialization parameter and cannot be modified after the database is initialized.
 - **Enable strong sync**: Strong sync (downgradable) and async are supported. For more information, see [Strong Sync](https://intl.cloud.tencent.com/document/product/1042/33318).
 - For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1042/35777).
2. After making the payment, return to the instance list. After the status of the instance changes to **Running**, it can be used normally.
![](https://qcloudimg.tencent-cloud.cn/raw/4ad820a453b3b55b9b3039b4ab13655a.png)

## Subsequent operations
For more information on how to connect to a TDSQL for MySQL instance at the private or public network address, see [Connecting to Instances](https://intl.cloud.tencent.com/document/product/1042/33338).
