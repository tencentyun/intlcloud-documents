### How do I connect to my TencentDB for Redis instance if it is deployed in the same region as the CVM instance?
In this case, please use the private network for access. For more information, please see [Connecting to Database Instance](https://intl.cloud.tencent.com/document/product/239/9897).

### How do I connect to my TencentDB for Redis instance if it is deployed in a different region from the CVM instance?
For communication between basic network and VPC, please see [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
For communication between VPCs, please see [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).

### What should I do if my TencentDB for Redis instance is unpingable? 
Redis prohibits `ping` by default. You can use telnet to check connectivity.

### How do I enable access to TencentDB for Redis over the public network? 
TencentDB for Redis does not support public network access for the time being. If you want to access it over the public network, you can do so through the [iptable proxy](https://intl.cloud.tencent.com/document/product/239/35905) on a CVM instance that has public network access.
>iptable-based forwarding may be unstable; therefore, you are not recommended to access instances over the public network in the production environment.
