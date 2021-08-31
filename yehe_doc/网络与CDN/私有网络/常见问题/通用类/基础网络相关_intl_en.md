### What is the difference between a classic network and a VPC?
- A Virtual Private Cloud (VPC) is a logically isolated network space in Tencent Cloud.
- VPCs provides more features than the classic network. For more information on their differences and how to choose between them, see [Managing Classic Networks](https://intl.cloud.tencent.com/document/product/215/31807).

### Can I switch a CVM from a classic network to a VPC? 
Yes. Tencent Cloud allows you to migrate one CVM or a batch of CVMs from a classic network to a VPC. For detailed steps and instructions, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
>!This operation cannot be undone. Be sure to carefully read the document before performing this operation.

### Can I switch a CVM from a VPC to a classic network?
No. A VPC supports more features with greater flexibility, and therefore we recommend that you migrate CVMs from the classic network to the VPC.

### How can I establish communication between a classic network CVM and a VPC-based CVM?
You can use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) to establish communication between the classic network and the VPC.
Using Classiclink is subject to the following limitations:
1. Both the classic network and the VPC to be communicated with are located in the same region (they can be in different availability zones, such as Guangzhou Zone 1 and Guangzhou Zone 2).
2. The VPC CIDR block (IP range) must be within `10.[0-47].0.0/16` (including subsets). Otherwise, there will be conflicts.

If your classic network and VPC meet these conditions, you can configure Classiclink on the VPC details page in the console, to associate the VPC with the classic network CVMs for interconnection.

### Can resources such as cloud load balancers and databases in the classic network communicate with the VPC?
- A terminal connection helps to establish communication between instances in a VPC and other instances in a classic network through the private network. It maps classic network instance IP addresses to VPC IP addresses, allowing you to access the classic network instances through a VPC IP address. Classic network products including classic CLB, TencentDB, CMEM, REDIS, and MongoDB can communicate with the VPC in this way. Cross-region and cross-account communication is not supported.
- Direction: One-way (the VPC accesses the classic network).
- If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply.

### Can classic networks and VPC instances under different accounts communicate with each other?
No. A VPC supports more features with greater flexibility, and therefore we recommend that you migrate resources from the classic network to the VPC.

### How can I unassociate a CVM from a VPC or a classic network?
Perform the following steps to unassociate a CVM.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. Click the ID of the VPC that is interconnected with the classic network to enter the VPC details page.
3. Click **Classiclink**. In the list of classic network CVMs, select the CVM to be unassociated and click **Disassociate**.
4. Click **OK**.

For step-by-step instructions, see the “Unassociating a VPC and Classic Network CVM” section in [Managing Classic Networks](https://intl.cloud.tencent.com/document/product/215/31807).
