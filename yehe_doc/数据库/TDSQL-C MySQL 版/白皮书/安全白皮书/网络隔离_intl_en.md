TDSQL-C supports the use of VPC to achieve a higher degree of network isolation and control. Using [security group](https://intl.cloud.tencent.com/document/product/213/12452) and [VPC](https://intl.cloud.tencent.com/document/product/215/535) together can greatly improve the security of access to TDSQL-C.

A VPC is a logically isolated network space established for users in Tencent Cloud. In a VPC, you can freely define IP range segmentation, IP addresses, and routing policies to achieve resource-level network isolation.

TDSQL-C instances deployed in a VPC can only be accessed by CVM instances in the same VPC by default. If the CVM and TDSQL-C instances are in different VPCs, they can communicate after you apply for public network access. For network security considerations, we recommend you not access your databases over the public network. If you have to do so, configure appropriate security groups to implement access control for clients.

