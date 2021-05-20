A VPC is a logically isolated virtual network that you can use exclusively and plan independently on Tencent Cloud. To use any Tencent Cloud resource, you must create a VPC and subnet. A subnet is a network space in the VPC. You can divide a VPC into at least one subnets. The VPC is regional, while the subnet is specific to the availability zone. Subnets in the same VPC can communicate with each other over a private network by default.

All cloud resources such as CVMs and CLBs in a VPC must be deployed in a subnet.


## Lifecycle of VPC
The VPC lifecycle varies with needs, as shown below:
![](https://main.qcloudimg.com/raw/68556cee99a7ececc3936b45cdaa3ca5.svg)
1. [Creating a VPC](https://intl.cloud.tencent.com/document/product/215/31805): you need to carefully [plan your network](https://intl.cloud.tencent.com/document/product/215/31795) before creating a VPC. The CIDR blocks of VPCs and subnets cannot be modified after creation.
2. [Viewing a VPC](https://intl.cloud.tencent.com/document/product/215/40069): you can view the basic information of a VPC, its CCN association, and the resources it contains.
3. (Optional) Choose the operations that apply to your use cases:
 - When the primary CIDR block is insufficient, see [Editing IPv4 CIDR Blocks](https://intl.cloud.tencent.com/document/product/215/40070):
    - [Creating secondary CIDR blocks](https://intl.cloud.tencent.com/document/product/215/40070#21): you can create secondary CIDR blocks to meet your actual network demands.
    - [Deleting secondary CIDR blocks](https://intl.cloud.tencent.com/document/product/215/40070#32): you can delete secondary CIDR blocks if you no longer need them.
4. [Deleting a VPC](https://intl.cloud.tencent.com/document/product/215/40073): after a VPC is deleted, its subnets and route tables are also deleted.

