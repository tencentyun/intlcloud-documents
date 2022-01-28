This document describes how to migrate a instance from the classic network to VPC and configure the hybrid access solution during the migration.

## Migrating a Single Instance
You can easily migrate a instance from the classic network to a VPC. See below for details.
<table >
<th>Instance type</th>
<th>Description</th>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278>CVM</a></td>
<td> <li>The instance will be restarted.<li>The classic network IP will immediately convert to a VPC IP.</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>TencentDB for MySQL</a></td>
<td rowspan=5>Both the classic network IP and VPC IP are available for a period of time. The original classic network IP remains valid as follows: <ul><li>MySQL:  default period: 24 hours (1 day); maximum period: 168 hours (7 days)<li>MariaDB:  valid for 24 hours (1 day)<li>TDSQL:  valid for 24 hours (1 day)<li>Redis:  available options: release now, release after 1 day, release after 2 days, release after 3 days, and release after 7 days<li>MongoDB:  the original IP address will become invalid immediately for version 4.0 or later. Other versions support the options: release now, release after 1 day, release after 2 days, release after 3 days, and release after 7 days</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>TencentDB for MariaDB</a></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>TDSQL for MySQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>TencentDB for Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/40126>TencentDB for MongoDB</a></td>
</tr>
</table>

>? If you want to keep the resource IP addresses unchanged after the network switch, try to create a VPC that has the classic network IPs. If this attempt is impossible, refer to the following solution:
+ Create a private DNS service and resolve its domain name. After migrating the resources to a VPC, use Tencent Cloud [private DNS](https://intl.cloud.tencent.com/document/product/1097/40551).
+ Use a public IP. 
## Hybrid Access Solution During the Migration
Hybrid access means the services being migrated can access both the classic network and a VPC. Tencent Cloud provides the following hybrid access solution:
+ The accessibility of classic network IP and VPC IP of the TencentDB service ensures the hybrid access at the TencentDB instance level.
    ![](https://main.qcloudimg.com/raw/e48e84309c8ff4494f5046f52cfce084.png)
+ The Cloud Object Storage (COS) access through domain name provides the hybrid access capability.
+ To implement interconnection during the migration, use together with:
  + Classiclink:  allows the classic network-based CVMs to interconnect with VPC resources such as CVM, TencentDB, and CLB instances.
  + Terminal connection:  allows the instances in a VPC to communicate with resources in the classic network (except CVMs).
  ![](https://main.qcloudimg.com/raw/a8c5d3ee6520a0b8992d23b1717a86d0.png)
   >? 
   >+ If you want to establish a terminal connection, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). This feature only supports accessing classic network-based CVMs. We recommend migrating your resources to a VPC.
   >+ To learn more about VPC and Classiclink solutions, see [Communicating with Classic Network](https://intl.cloud.tencent.com/document/product/215/35505). For more information about how to configure a Classiclink, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).

