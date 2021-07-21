This document describes how to migrate a CVM, TencentDB for MySQL instance, and TencentDB for Redis instance from the classic network to a VPC.

## Background
- The classic network is a public network resource pool for all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.
- A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies, making it more suitable for use cases requiring custom configurations.

As the classic network resources become increasingly scarce and cannot be expanded, starting from June 13, 2017, all new-registered Tencent Cloud accounts can only create instances (including CVM and TencentDB instances) in a VPC rather than the classic network. More and more users are migrating their instances from the classic network to VPC.


## Directions
Check the instructions below according to your resource type.
<table>
<thead>
<tr>
<th width="20%">Resource Type</th>
<th width="25%">Characteristics</th>
<th width="35%">Limitation</th>
<th width="20%">Instruction</th>
</tr>
</thead>
<tbody><tr>
<td>CVM</td>
<td>The migrated CVM instances are the same as those being created in the VPC.</td>
<td><li>Migrating from classic network to VPC CANNOT be reverted. After the migration, the CVM instance cannot communicate with Tencent Cloud services in the classic network</li>
<li>The CVM instance needs to be restarted</li>
<li>The private IP changes from the classic network IP to VPC IP</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/20278" target="_blank">Switch to VPC</a></td>
</tr>
<tr>
<td>TencentDB for MySQL</td>
<td><li>The VPC access takes effect immediately after the migration.</li><li>The original classic network remains accessible for up to 7 days after the migration.</li><li>The database connection is not affected during the migration.</li></td>
<td><li>Migrating from the classic network to VPC CANNOT be reverted. After the migration, the TencentDB for MySQL instance cannot communicate with Tencent Cloud services in the classic network</li>
<li>The private IP changes from the classic network IP to VPC IP.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Switch Network</a></td>
</tr>
<tr>
<td>TencentDB for Redis</td>
<td><li>The VPC access takes effect immediately after the migration.</li><li>The original classic network remains accessible for up to 7 days after the migration.</li><li>The database connection is not affected during the migration.</li></td>
<td><li>Migrating from the classic network to VPC CANNOT be reverted. After the migration, the TencentDB for Redis instance cannot communicate with Tencent Cloud services in the classic network</li>
<li>The private IP changes from the classic network IP to VPC IP.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31944?from=10680#.E6.9B.B4.E6.8D.A2-redis-.E7.BD.91.E7.BB.9C" target="_blank">Change Redis Network</a></td>
</tr>
</tbody></table>

## Migration Sample
>?This example is only for reference. Before your actual migration, please assess the impact on your business and develop a detailed migration plan .
### Description

Suppose a classic network-based service uses four Tencent Cloud services, including CLB, CVM, TencentDB for MySQL, and TencentDB for Redis. Their relationship is shown below: 
- The public CLB is bound with two CVMs as the backend servers.
- TencentDB for MySQL and TencentDB for Redis act as databases for applications deployed in the two CVMs.
![](https://main.qcloudimg.com/raw/bf54dd1832d0e16c756984e305772e06.png)

## Migration Directions
1. Migrate TencentDB instances to a VPC. After the migration, the original classic network access remains available for a certain period, thus maintaining the database connection and your service availability. During this period, you can complete the migration of other services.
![](https://main.qcloudimg.com/raw/427fe3f0445056c94332df90d4cd9bb3.png)
2. Create two CVMs and deploy services as needed in the VPC where the databases are migrated to. Then test whether the CVMs can access TencentDB instances.
![](https://main.qcloudimg.com/raw/4425f9af34e3df70a84f1a80e8a7ba40.png)
3. Create a public CLB in the VPC of databases, and associate it with the two CVMs created in the previous step. Perform a health check to avoid service interruption due to an exception.
![](https://main.qcloudimg.com/raw/8dab2d96a40f1df4eefa9ad04117cb2b.png)
4. Wait for the migration to complete. Release the original public network CLB and CVM resources in the classic network.
![](https://main.qcloudimg.com/raw/cb567a4a3f88c4bc4c8d787d60f512f3.png)

