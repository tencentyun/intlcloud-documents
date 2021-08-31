### What is Classiclink?
The Classiclink is used to associate CVMs in the classic network to the specific VPC, enabling CVMs to communicate with Tencent Cloud services including CVMs and databases in the VPC. For more information, see [Managing Classic Networks](https://intl.cloud.tencent.com/document/product/215/31807).

### How can I establish communication between a CVM in a classic network and a CVM in a VPC?
You can use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) to establish communication between classic networks and VPCs.
When using the Classiclink, take note of the following limits:
1. The classic network and the VPC that need to communicate with each other must be in the same region (but can be in different availability zones, such as Guangzhou Zone 1 and Guangzhou Zone 2).
2. The CIDR (IP range) of the VPC must be `10.0.0.0/16 - 10.47.0.0/16` (including subsets), otherwise a conflict occurs.

If your classic network and VPC meet these conditions, you can configure the **Classiclink** tab on the details page of the VPC in the Console to associate the VPC with the CVMs in the classic network for interconnection.

### Can resources including cloud load balancers and databases in the classic network communicate with the VPC?
- A terminal connection helps establish communication between instances in a VPC and other instances in a classic network over a private network. The principle is to map the IP addresses of instances in the classic network to VPC IP addresses so that you can access a classic network instance by accessing the corresponding VPC IP address. The services that support the classic network include classic CLB, TencentDB, CMEM, REDIS, MongoDB. Cross-region/cross-account communication is not supported.
- Direction: one-way (VPC accesses the classic network).
- If you need more directions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply.

### Can classic network and VPC instances under different accounts communicate with each other?
No. Currently, resources (CVMs and databases) in classic networks and VPC instances under different accounts cannot communicate with each other. A VPC supports more features with greater flexibility, so we recommend migrating from the classic network to VPC.
