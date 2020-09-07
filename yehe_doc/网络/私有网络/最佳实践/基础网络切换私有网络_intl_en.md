This document describes how to migrate Cloud Virtual Machine (CVM), TencentDB for MySQL, and TencentDB for Redis from a classic network to VPC.

## Background
- The classic network is the public network resource pool for all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.
- A Virtual Private Cloud (VPC) is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies, making it more suitable for use cases requiring custom configurations.

Due to the growing scarcity and non-expansion of the classic network resources, Tencent Cloud accounts registered after June 13, 2017 can only create instances (including CVM and TencentDB) in a VPC, but not in the classic network. More and more users are migrating their instances from the classic network to VPC.


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
<td><li>The VPC access takes effect immediately after the migration</li><li>The original classic network remains accessible for up to 24 hours after the migration</li><li>The database connection is not affected during the migration</li></td>
<td><li>Migrating from classic network to VPC CANNOT be reverted. After the migration, the TencentDB for MySQL instance cannot communicate with Tencent Cloud services in the classic network</li>
<li>The private IP changes from the classic network IP to VPC IP</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">Network Switch</a></td>
</tr>
<tr>
<td>TencentDB for Redis</td>
<td><li>The VPC access takes effect immediately after the migration</li><li>The original classic network remains accessible for up to 7 days after the migration</li><li>The database connection is not affected during the migration</li></td>
<td><li>Migrating from classic network to VPC CANNOT be reverted. After the migration, the TencentDB for Redis instance cannot communicate with Tencent Cloud services in the classic network</li>
<li>The private IP changes from the classic network IP to VPC IP</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31944" target="_blank">Configure Network</a></td>
</tr>
</tbody></table>

## Migration Sample
### Description
This example is only for reference. In actual migration, please carefully assess the impact and develop the migration plan in advance.
Suppose a classic network-based service uses four Tencent Cloud services, including CLB, CVM, TencentDB for MySQL, and TencentDB for Redis, as shown below: 
- The public CLB is bound with two CVMs as the backend servers.
- TencentDB for MySQL and Redis act as databases for applications deployed in the two CVMs.
![](https://main.qcloudimg.com/raw/bf54dd1832d0e16c756984e305772e06.png)

## Migration Directions
1. Migrate TencentDB instances to a VPC. After the migration, the original classic network access remains available for a certain period, so as to maintain the database connection and and your service availability. During this period, you can complete migration of other services.
![](https://main.qcloudimg.com/raw/427fe3f0445056c94332df90d4cd9bb3.png)
2. In the VPC where the databases are migrated to, create two CVMs and deploy services as needed. Then test whether the CVMs can access TencentDB instances.
![](https://main.qcloudimg.com/raw/4425f9af34e3df70a84f1a80e8a7ba40.png)
3. In the VPC of databases, create a public CLB and associate it with the two CVMs created in the previous step. Perform health check to avoid service interruption due to an exception.
![](https://main.qcloudimg.com/raw/8dab2d96a40f1df4eefa9ad04117cb2b.png)
4. Wait for the migration to complete. Release the original public network CLB and CVM resources in the classic network.
![](https://main.qcloudimg.com/raw/cb567a4a3f88c4bc4c8d787d60f512f3.png)
