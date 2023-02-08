TDSQL-C for MySQL provides data communication security capabilities to ensure the confidentiality and integrity of data during communication.

## VPC
TDSQL-C for MySQL supports using Virtual Private Cloud (VPC) to achieve a higher degree of network isolation and control. A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies to implement network isolation at the resource level.

Read-write instances and read-only instances in a TDSQL-C for MySQL cluster deployed in a VPC can only be accessed by CVM instances in the same VPC by default. If the CVM and instances are in different VPCs, they can communicate after you apply for public network access. For the sake of network security, we recommend you not access your databases over the public network. If you have to do so, configure appropriate security groups to implement access control for clients.

For more information on the feature, see [VPC Overview](https://intl.cloud.tencent.com/document/product/215/535).

## Security group
TDSQL-C for MySQL supports security group as an important means for network security isolation, which can be used to set network access controls for one or more instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group.

For more information on how to use this feature, see [Creating and Managing TencentDB Security Groups](https://www.tencentcloud.com/document/product/1098/52007).
