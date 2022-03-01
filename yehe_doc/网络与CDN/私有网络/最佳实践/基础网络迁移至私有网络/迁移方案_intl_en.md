This document describes how to migrate from your resources from the [classic network](https://intl.cloud.tencent.com/document/product/215/41417) to [VPC](https://intl.cloud.tencent.com/document/product/215/535).

>? 
> Before switching the network, you need to create a VPC in the same region as the classic network instance to be migrated and create a subnet in the same AZ as the instance. For more information, see [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).

Tencent Cloud provides the two migration solutions below:
+ Migrating a ingle instance: Choose this if you only need to migrate instances one by one.
+ Hybrid access: if your business involves CVM, CLB, and TencentDB instances, you can use this solution to ensure a smooth business migration.

## Migrating a Single Instance
You can easily migrate a instance from the classic network to a VPC. See below for details.
<table >
<tr>
<th width="25%">Instance</th>
<th>Features</th>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278>CVM</a></td>
<td> <ul><li>The instance needs to be restarted</li><li>The classic network IP is immediately changed to the VPC IP, with no retention time</li><li>If the CVM instance has a public IP, the public IP will stay unchanged after the network switch, which will not affect the access at domain name</li></ul></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>TencentDB for MySQL</a></td>
<td rowspan=5>Dual-IP access is maintained for a certain period of time. The original classic network IP retention time is as follows: <ul><li>MySQL: 24 hours (1 day) by default and up to 168 hours (7 days) <li>MariaDB: 24 hours (1 day) <li>TDSQL: 24 hours (1 day) <li>Redis: you can choose to expire immediately, release after 1 day, release after 2 days, release after 3 days, or release after 7 days <li>MongoDB: the original IP on v4.0 or above will expire immediately. For other versions, you can choose to expire immediately, release after 1 day, release after 2 days, release after 3 days, or release after 7 days</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>TencentDB for MariaDB</a></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>TDSQL for MySQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>TencentDB for Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/44180>TencentDB for MongoDB</a></td>
</tr>
<tr>
<td><a href=>TencentDB for PostgreSQL</a> </td>
<td>You can configure up to two networks for each instance, both of which can be used for business access. The IPs of different networks can be the same.</td>
</tr>
</table>

>? If you want to keep the resource IP addresses unchanged after the network switch, try to create a VPC that covers the classic network IP. 
+ Create a private DNS service and resolve its domain name. After migrating the resources to a VPC, use Tencent Cloud [Private DNS](https://intl.cloud.tencent.com/document/product/1097/40551).
+ Access using the public IP. 
## Hybrid Access Solution During the Migration
Hybrid access means the services being migrated can access both the classic network and a VPC. Tencent Cloud provides the following hybrid access solutions:
+  TencentDB: the accessibility of classic network IP and VPC IP ensures the hybrid access at the TencentDB instance level.
    ![](https://main.qcloudimg.com/raw/e48e84309c8ff4494f5046f52cfce084.png)
+ COS: access through domain name naturally provides the hybrid access capability.
+ CVM:
 + Classiclink: allows the classic network-based CVMs to interconnect with VPC resources such as CVM, TencentDB, and CLB instances.
 + Peering connection: allows the instances in a VPC to communicate with resources in the classic network (except CVMs).
![](https://main.qcloudimg.com/raw/a8c5d3ee6520a0b8992d23b1717a86d0.png)
>?
>+ To use peering connection, [submit a ticket](https://console.cloud.tencent.com/workorder/category). 
>+ To configure Classiclink, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
>+ For migration of CLB instances, see [Example: Migrating a Public Network CLB](https://intl.cloud.tencent.com/document/product/215/41415) and [Example: Configuring Hybrid Access for a Private Network CLB](https://intl.cloud.tencent.com/document/product/215/41416).
