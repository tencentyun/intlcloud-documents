The classic network is a public network resource pool for all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses. The VPC with an independent, controllable and more secure access are evolved from the classic network to meet the requirements of a growing number of users for more complex services.
>?As the classic network resources become increasingly scarce and cannot be expanded, Tencent Cloud accounts registered after June 13, 2017, 00:00:00 can create instances (including CVM and CLB) only in a VPC rather than the classic network.  If you need to use classic network service, please submit an application.


## Use Limits
+ The classic network-based CVMs do not support ENIs.
+ Migrating from the classic network to VPC is irreversible.

## Classic Network vs. VPC
Both classic network and VPC are network spaces on the cloud.  
+ The classic network is a public network resource pool for all Tencent Cloud users (as shown on the right side of the figure below). The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.
+ By contrast, the VPC is a logically isolated network space in Tencent Cloud (as shown on the left side of the figure below). In a VPC, you can customize IP ranges, IP addresses, and routing policies. VPC is more suitable for use cases requiring custom configurations.
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

>?You can use the [`DescribeAccountAttributes`](https://intl.cloud.tencent.com/document/product/215/17875) API to query the network attributes of an account.  If the `supportedPlatforms` value is `only-vpc`, the account is a default VPC user, who owns all cloud resources under VPCs. If the `supportedPlatforms` value is `classic`, the account is a default classic network user, who owns all cloud resources under the classic network.

## Reference
+ For more information about the communication plan between a VPC and the classic network, see [Communicating with Classic Network](https://intl.cloud.tencent.com/document/product/215/35505).
+ For more information about Classiclink configurations, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
+ You can migrate your instances from the classic network to a VPC. For detailed directions, see [Migrating from the Classic Network to VPC](https://intl.cloud.tencent.com/document/product/215/41414).

