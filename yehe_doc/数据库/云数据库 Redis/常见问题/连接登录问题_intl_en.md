### How do I connect to a TencentDB for Redis instance?
You can connect to a TencentDB for Redis instance using a client tool, the database management center (DMC), and SDKs supporting various programing languages. For more information, see [Connecting to TencentDB for Redis Instances (over Private Network)](https://intl.cloud.tencent.com/document/product/239/9897).

### What should I do if the connection to TencentDB for Redis failed?
Common causes of connection failure: network/security group issues, password issues, and connection issues (i.e., the maximum number of connections has been reached). For corresponding solutions, see [Redis Instance Connection Failure](https://cloud.tencent.com/document/product/239/58020).

### How can TencentDB for Redis support private network access? How do I view the private network address of my instance?
To support private network access, the CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.

To view the private network address, log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), view the address in the instance list, or click an instance ID and view the address on the displayed instance details page.

### Can my CVM instance connect to TencentDB for Redis over private network?
1. The following conditions must be met to use the private network connection:
The CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.
2. You can check whether they are in the same VPC or both in the classic network in the following ways:
 - You can log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance), and view the network information of a CVM instance in the instance list or on the instance details page.
 - You can log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), and view the network information of a Redis instance in the instance list or on the instance details page.
 For more information, see [Viewing network type and VPC information](https://cloud.tencent.com/document/product/239/58020#wllxvpdff).

### What should I do if my CVM and TencentDB for Redis instances are in different VPCs?
You can connect to instances through CCN.
CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Cloud Connect Network](https://cloud.tencent.com/document/product/877).

### My CVM and TencentDB for Redis instances are in different regions (such as Guangzhou and Shanghai, respectively). Can I use a private network for connection?
If CVM and Redis instances are in different [regions](https://intl.cloud.tencent.com/document/product/239/4106), they are in different VPCs, so they cannot interconnect directly over private network. We recommend that you use [CCN](https://cloud.tencent.com/document/product/877) to connect the VPCs.

### My CVM and TencentDB for Redis instances are in different AZs (such as Shanghai Zone 2 and Shanghai Zone 1, respectively) in the same region. Can I use a private network for connection?
Even if the CVM and TencentDB for Redis instances are in the same region, they may be in different VPCs.
- If they are in different AZs in the same VPC, they can interconnect over private network.
- If they are in different VPCs (such as VPC 1 and VPC 2, respectively), they cannot interconnect over private network. For solutions, see [Redis Network Change](https://intl.cloud.tencent.com/document/product/239/31944).

### My CVM and TencentDB for Redis instances are in different AZs (such as Shanghai Zone 2 and Shanghai Zone 1, respectively) in the same VPC. Can I use a private network for connection?
Yes. Instances in different AZs but in the same VPC interconnect over private network by default.

### My CVM and TencentDB for Redis instances are under different accounts. Can I use a private network for connection?
No. Because instances under different accounts are in different VPCs. We recommend that you use [CCN](https://cloud.tencent.com/document/product/877) for connection.

### How do I enable access to Redis over public network? 
For more information, see [Configuring Public Network Address](https://cloud.tencent.com/document/product/239/63527).

