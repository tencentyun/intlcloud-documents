### What Is the Difference Between the Basic Network and the VPC?
- A VPC is a logically isolated network space that you can establish on Tencent Cloud.
- A VPC provides more features than the basic network. For details on their differences and how to choose between them, see [Managing the Basic Network](https://intl.cloud.tencent.com/document/product/215/31807).

### Can I Change the Attribute of a CVM from Basic Network to VPC?
Yes, you can do this by using the service of switching a single CVM or a batch of CVMs from the basic network to VPC instances. For detailed steps and instructions, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
-> This operation cannot be undone. Be sure to carefully read the document before performing this operation.

### Can I Change the Attribute of a CVM from VPC to Basic Network?
No, you cannot. Currently, changing the attribute of a CVM from VPC to basic network is not supported. A VPC supports more features with greater flexibility, and therefore we recommend that you migrate from the basic network to the VPC.

### How Can I Establish Communication Between a CVM in the Basic Network and a CVM in a VPC?
You can use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) to establish communication between the basic network and the VPC.
Using Classiclink is subject to the following limitations:
1. The basic network and the VPC that need to communicate with each other must be in the same region (but can be in different availability zones, such as Guangzhou Zone 1 and Guangzhou Zone 2).
2. The CIDR block (IP address range) of the VPC must be `10.[0-47].0.0/16` (including subsets), otherwise a conflict occurs.

If your basic network and VPC meet these conditions, you can configure the settings in the Classiclink area on the details page of the VPC in the console, to associate the VPC with the CVMs in the basic network for interconnection.

### Can Resources Such as Cloud Load Balancers and Databases in the Basic Network Communicate with the VPC?
- A terminal connection helps establish communication between instances in a VPC and other instances in a basic network through the private network. Here, the principle is to establish mapping between basic network instance IP addresses and VPC IP addresses so that you can access a basic network instance by accessing the corresponding VPC IP address. Supported basic network products include CLB, TencentDB, CMEM, REDIS, and MongoDB. Cross-region and cross-account communication is not supported.
- Direction: one-way (the VPC accesses the basic network.)
- If you need more directions, submit a [ticket](https://console.cloud.tencent.com/workorder/category) to apply.

### Can Basic Networks and VPC Instances Under Different Accounts Communicate with Each Other?
Currently, communication between resources (CVMs and databases) of basic networks and VPC instances under different accounts is not supported. A VPC supports more features with greater flexibility, and therefore we recommend that you migrate from the basic network to the VPC.

### How Can I Disassociate a CVM from a VPC or Basic Network?
The disassociation procedure is as follows:
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc/vpc).
2. Click the ID of the VPC that is interconnected with the basic network to enter the VPC details page.
3. Click **Classiclink**. In the list of basic network CVMs, select the CVM to be disassociated and click **Unassociate**.
4. Click **OK** to complete the disassociation.

For step-by-step instructions, see [Disassociating CVMs from a VPC or Basic Network](https://intl.cloud.tencent.com/document/product/215/20154).
