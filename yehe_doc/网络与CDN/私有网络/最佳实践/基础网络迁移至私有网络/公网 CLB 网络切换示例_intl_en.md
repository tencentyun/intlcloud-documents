This document describes how to smoothly migrate your public network CLB service from the classic network to a VPC.
>? This example is only for reference. In actual migration, please carefully assess the impact and develop the migration plan in advance.

### Scenario
Resource configuration of the classic network-based business: 
+ The DNS domain name is resolved to the public network CLB’s VIP in the classic network.
+ The public network CLB is bound with two CVMs (CVM 1 and CVM 2) as the backend servers.
+ Applications deployed in CVM 1 and CVM 2 can access the backend TencentDB for Redis and TencentDB for MySQL services.


### Migration process
<dx-steps>
- Create a VPC
- Migrate TencentDB services
- Create CVM instances and deploy applications
- Create a public network CLB and associate it with the CVMs
- Change the IP address of the DNS domain name
- Release the classic network resources
</dx-steps>

### Migration directions
1.  Create a VPC as instructed in [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).
![]()
2.  Migrate [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/31915) and [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/31944) instances to the VPC.
>? During the migration, the TencentDB instances is still connected. Both the original classic network IP and VPC IP addresses remain valid for a certain period after the migration, thus maintaining your service availability. Please complete the migration of other resources within the period.
>
![]()
3.  Create images for the classic network-based CVM 1 and CVM 2 as instructed in [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942) and [use the images](https://intl.cloud.tencent.com/document/product/213/36304) to create two CVM instances in the VPC. Then test whether the CVMs can access TencentDB instances.
 >? If restarting CVM instances during the migration is acceptable to your business, you can directly switch to VPC during off-peak hours. For detailed directions, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
 >
![]()
4.  Create a public network CLB in the VPC and associate it with the two CVMs created in the previous step. For more information, see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). Perform a health check to avoid service interruption due to an exception.
![]()
5.  Resolve the DNS domain name to the public network CLB’s VIP in the VPC.
![]()
6.  Check whether the VPC works well. If yes, release the original public network CLB and CVM resources in the classic network to finish the migration.
 >? The original classic network IP of a TencentDB instance will be automatically released after expiration.
 >
![]()
