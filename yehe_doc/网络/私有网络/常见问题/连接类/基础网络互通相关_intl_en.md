### What Is Classiclink?
Classiclink is designed to associate CVMs in the basic network with specified VPC instances, allowing the CVMs to communicate with cloud services in the VPC instances such as CVMs and databases. For more information, see [Managing the Basic Network](https://intl.cloud.tencent.com/document/product/215/31807).

### How Can I Establish Communication Between a CVM in the Basic Network and a CVM in a VPC?
You can use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) to establish communication between the basic network and the VPC.
Using Classiclink is subject to the following limitations:
1. The basic network and the VPC that need to communicate with each other must be in the same region (but can be in different availability zones, such as Guangzhou Zone 1 and Guangzhou Zone 2).
2. The CIDR block (IP range) of the VPC must be `10.0.0.0/16 - 10.0.47.0/16` (including subsets), otherwise a conflict occurs.

If your basic network and VPC meet these conditions, you can configure the settings in the Classiclink area on the details page of the VPC in the console, to associate the VPC with the CVMs in the basic network for interconnection.

### Can Resources Such as Cloud Load Balancers and Databases in the Basic Network Communicate with the VPC?
- A terminal connection helps establish communication between instances in a VPC and other instances in a basic network through a private network. Here, the principle is to establish mapping between basic network instance IP addresses and VPC IP addresses so that you can access a basic network instance by accessing the corresponding VPC IP address. Supported basic network products include CLB, TencentDB, CMEM, REDIS, and MongoDB. Cross-region and cross-account communication is not supported.
- Direction: one-way (the VPC accesses the basic network.)
- If you need more directions, submit a [ticket](https://console.cloud.tencent.com/workorder/category) to apply.

### Can Basic Networks and VPC Instances Under Different Accounts Communicate with Each Other?
Currently, communication between resources (CVMs and databases) of basic networks and VPC instances under different accounts is not supported. VPC instances support more features with greater flexibility, and therefore we recommend that you migrate from the basic network to the VPC.
