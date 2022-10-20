TencentDB for MySQL provides data communication security capabilities to ensure the confidentiality and integrity of data during communication.

## [VPC](id:SYWL)
TencentDB for MySQL supports using Virtual Private Cloud (VPC) to achieve a higher degree of network isolation and control. A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies to implement network isolation at the resource level.

TencentDB for MySQL instances deployed in a VPC can only be accessed by CVM instances in the same VPC by default. If the CVM and MySQL instances are in different VPCs, they can communicate after you apply for public network access. For the sake of network security, we recommend you not access your databases over the public network. If you have to do so, configure appropriate security groups to implement access control for clients.

For more information on how to use this feature, see [Creating VPCs for TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/8468).

## [Security group](id:AQZ)
TencentDB for MySQL supports security group as an important means for network security isolation, which can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group.

For more information on how to use this feature, see [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).

## [SSL encryption](id:SSLJM)
TencentDB for MySQL supports Secure Sockets Layer (SSL) authentication, which is a process that authenticates the connection from the user client to the TencentDB server. After SSL encryption is enabled, you can get a CA certificate and upload it to the server. Then, when the client accesses the database, the SSL protocol will be activated to establish an SSL secure channel between the client and the server. This implements encrypted data transfer, prevents data from being intercepted, tampered with, and eavesdropped during transfer, and ultimately ensures the data security.

Note that SSL encryption does not protect the data itself; instead, it secures the traffic between the database and the server. Encrypting the network connection at the transport layer can improve the security and integrity of the communication data, but will increase the response time of the network connection.

For more information on how to use this feature, see [Setting SSL Encryption](https://intl.cloud.tencent.com/document/product/236/48452).
