
### What should I do if the connection to TencentDB for Redis failed?
>?
>- When a CVM instance is used to access the private network address of a TencentDB instance, both instances should be under the same account in the same VPC in the same region, or both in the classic network.
>- CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
>- TencentDB for Redis doesn't support public network address currently. To connect to TencentDB for Redis instances over public network, please see [iptables Forwarding](https://intl.cloud.tencent.com/document/product/239/35905).
>
Common reasons for connection failure are as follows:
- The TencentDB for Redis and CVM instances are under different accounts. They are better to be under the same account and in the same VPC in the same region.
- The TencentDB for Redis and CVM instances are in different regions. They are better to be under the same account and in the same VPC in the same region.
- The TencentDB for Redis and CVM instances are in different VPCs. Please change the network as instructed in [Configuring Network](https://intl.cloud.tencent.com/document/product/239/31944).
- The security group rule of the CVM instance blocks access to the private network address and port of the TencentDB for Redis instance. Please modify the rule as instructed in [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).

### How do I connect to my TencentDB for Redis instance if it is deployed in the same region as the CVM instance?
In this case, please use the private network for access. For more information, please see [Connecting to Instance (over Private Network)](https://intl.cloud.tencent.com/document/product/239/9897).

### How do I connect to my TencentDB for Redis instance if it is deployed in a different region from the CVM instance?
For communication between classic network and VPC, please see [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
For communication between VPCs, please see [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).

### What should I do if my TencentDB for Redis instance is unpingable? 
Redis prohibits `ping` by default. You can use telnet to check connectivity.

### How do I enable access to TencentDB for Redis over the public network? 
TencentDB for Redis doesn't support public network address currently. If you want to access it over the public network, you can do so through the [iptable proxy](https://intl.cloud.tencent.com/document/product/239/35905) on a CVM instance that has public network access.
>?Port forwarding with iptables is not stable, so we do not recommend this public network access solution in a production environment.

### How do I view the private network address?
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and view it in the instance list. You can also click an instance ID to enter the **Instance Details** page and view it.

