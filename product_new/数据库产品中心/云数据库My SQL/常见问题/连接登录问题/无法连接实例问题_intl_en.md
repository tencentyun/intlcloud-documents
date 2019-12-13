### Different Network Types
If the networks of a CVM instance and a TencentDB for MySQL instance are of different types, the former cannot access the latter directly over the private network.
#### The CVM instance uses a VPC, while the TencentDB for MySQL instance uses the basic network
- Solution 1 (**recommended**): Switch the TencentDB for MySQL instance from basic network to VPC.


>- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- The switch from basic network to VPC is irreversible.
>- After the switch, VPC access will take effect immediately. The original basic network access will be retained for 24 hours; therefore, other instances associated to the TencentDB for MySQL instance should be migrated to VPC within 24 hours so as to guarantee uninterrupted access.
- Solution 2: Purchase a new CVM instance that resides in the basic network (the existing CVM instance cannot be migrated from VPC to basic network). However, VPC is more secure than basic network and thus highly recommended.
- Solution 3: Connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, so you are recommended to use VPC.

#### The CVM instance uses the basic network, while the TencentDB for MySQL instance uses a VPC
- Solution 1 (**recommended**): Migrate the CVM instance from basic network to VPC. For more information on directions, see [CVM Migration Sample](https://intl.cloud.tencent.com/document/product/213/20278).


 >- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- You need to unbind private/public network CLB instances and ENIs and release auxiliary IPs of the primary ENI before migration and bind them again after migration.
>- The CVM instance will be restarted during migration. Do not perform other operations on it.
>- Check the instance status after migration and verify whether private network access and remote login work properly.
- The switch from basic network to VPC is irreversible. After the switch to a VPC, the CVM instance cannot communicate with Tencent Cloud services in basic network.
- Solution 2: [Use Classiclink](https://intl.cloud.tencent.com/document/product/215/20083).
- Solution 3: Connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, and you are recommended to use VPC.


### Different VPCs
 By default, the CVM and TencentDB for MySQL instances can interconnect over the private network only if they are in the same VPC. If they are in different VPCs, interconnection over the private network can be achieved in the following ways:
- Solution 1 (**recommended**): Migrate the TencentDB for MySQL instance to the VPC where the CVM instance resides.
For more information on directions, see [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915) for TencentDB for MySQL.
-  Solution 2: Create a [peering connection](https://intl.cloud.tencent.com/document/product/215/5000) between the two VPCs.
Otherwise, the instances can only interconnect over the public network, which has poor performance, security, and stability.

### Incorrect Security Group Configuration
If the security group of the CVM instance and the TencentDB for MySQL instance are incorrectly configured, the former cannot access the latter directly over the private or private network.

#### The security group of the CVM instance is incorrectly configured
To enable the CVM instance to access the TencentDB for MySQL instance over the private network, you need to configure an outbound rule in the security group of the CVM instance. **If the destination of the outbound rule isn't 0.0.0.0/0 and the protocol port isn't ALL**, the private IP and port of the TencentDB for MySQL instance should be added to the rule.
1. Go to the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM Console and click the name of the CVM-bound security group to enter its details page.
2. On the **Outbound Rules** tab, click **Add Rule**.
Enter your IP address (or range) and port to be opened (private network address of the TencentDB for MySQL instance) and select "Allow".

#### The security group of the TencentDB for MySQL instance is incorrectly configured
To enable the CVM instance to access the TencentDB for MySQL instance over the private or public network, you need to configure an inbound rule in the security group of the TencentDB for MySQL instance. **If the source of the inbound rule isn't 0.0.0.0/0 and the protocol port isn't ALL**, the private or public client IP and port of the CVM instance should be added to the rule. 
1. Go to the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM Console and click the name of the TencentDB for MySQL-bound security group to enter its details page.
2. On the **Inbound Rules** tab, click **Add Rule**.
Enter the allowed IP address (or range) and port to be opened (private network port of the TencentDB for MySQL instance) and select "Allow".


>- TencentDB for MySQL uses private network port 3306 by default and supports customizing the port. If the default port is changed, the new port should be opened in the security group.
>- For public network access to the TencentDB for MySQL instance, port 3306 of the instance should be opened in the inbound rule of the security group.
>- In addition, the public client IP address should be added to the inbound rule of the security group.

