## Overview
CCN can interconnect a VPC with another VPC or a local IDC. To use CCN access, you must establish cross-VPC and VPC-IDC interconnections through CCN in advance.

In this scenario, you have used CCN to interconnect the three networks of VPC-Guangzhou, VPC-Chengdu, and VPC-Shanghai, have a self-built database in Guangzhou, and plan to migrate the data in the source database in Guangzhou to the target database in Nanjing. VPC-Chengdu is selected as the **Accessed VPC**.

## Configuration principles

When selecting CCN access, you need to connect the source database to the source of the DTS migration/sync linkage over CCN as follows: source database > accessed VPC > source of the migration/sync linkage, as shown in orange below.

<img src="https://qcloudimg.tencent-cloud.cn/raw/731aafbd4595e86f9a59ba173f0e4662.jpg" style="zoom:67%;" />

The accessed VPC and the source of the migration/sync linkage are interconnected as follows in the entire DTS task:

- The source of the migration/sync linkage is the network in the region of the source database selected during the task purchase, as shown below:
   The region of the source database selected during task purchase must be the same as the region of the accessed VPC; otherwise, the networks cannot be interconnected, and DTS will change the former to the latter.
  <img src="https://qcloudimg.tencent-cloud.cn/raw/be0a5f791aa2c827a7936d01bd48cc5f.png" style="zoom:50%;" />

- Accessed VPC: The accessed VPC refers to the VPC in CCN over which the migration/sync linkage is connected. It can be configured when you set the source and target databases as shown below:
   The accessed VPC and the VPC of the source database are interconnected over CCN.


## Directions
Establish interconnections as instructed in [Connecting Network Instances Under the Same Account](https://intl.cloud.tencent.com/document/product/1003/31986).

> ?CCN only provides bandwidth below 10 Kbps between all regions free of charge. However, DTS requires a higher bandwidth. Therefore, bandwidth configuration in the link is required.

## Subsequent operations
1. To perform a [data migration task](https://intl.cloud.tencent.com/document/product/571/42645) or [data sync task](https://intl.cloud.tencent.com/document/product/571/47344), you need to configure relevant parameters. Here, data migration from MySQL is used as an example. In the **Set source and target databases** step of the data migration task, select **CCN** and configure key parameters as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/30832fef580f406d0e19b6e0329724e6.png" style="zoom:50%;" />
<table>
<thead><tr><th><strong>Parameter</strong></th><th><strong>Description</strong></th><th><strong>Sample Value</strong></th></tr></thead>
<tbody>
<tr>
<td>Host Address</td><td>IP address of the source database server.</td><td>172.16.0.0</td></tr>
<tr>
<td>Port</td>
<td>Port used by the source database. Below are the default ports for common databases (if they are modified, enter the actual ports): <ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
<tr>
<td>VPC-based CCN Instance</td><td>CCN instance name.</td><td>ccn6-xxxx7d</td></tr>
<tr>
<td>Accessed VPC</td>
<td>The accessed VPC refers to the VPC in CCN over which the migration/sync linkage is connected. You need to select a CCN-associated VPC other than the VPC where the source database resides.<br>For example, if the database in Guangzhou region is selected as the source database, you should select <b>VPC-Chengdu</b> or <b>VPC-Shanghai</b> as the <b>accessed VPC</b>. Here, <b>Chengdu-VPC</b> is selected.</td>
<td>VPC-Chengdu</td></tr>
<tr>
<td>Subnet</td>
<td>Name of the subnet of the selected VPC.<br>If you cannot pull the subnet, there may be a problem with your account. The account of the accessed VPC must be the same as the migration account.<br>For example, to migrate a database under account A to account B, you should use account B to create a task. Therefore, the accessed VPC must be under account B.</td>
<td>VPC-Chengdu-Subnet</td></tr>
<tr>
<td>Region of Accessed VPC</td><td>The region of the source database selected during task purchase must be the same as the region of the accessed VPC; otherwise, DTS will change the former to the latter.</td><td>Chengdu</td></tr>
</tbody></table>
2. Click **Test Connectivity**. If the test fails, troubleshoot as follows:
   - The Telnet test fails.
     In the CCN-associated VPC (VPC-Chengdu in this example), purchase a CVM instance and ping the source database server address from it:
     - If the address is unpingable:
      - The server where the source database resides has a security group or firewall configured as described in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552).
      - The SNAT IP address is blocked in the source database as described in [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552).
      - The port settings of the source database are incorrect.
      - Some route tables in the CCN instance are not enabled due to IP range conflicts.
     - If the address is pingable, the routing between the source database and CCN is normal.     
      - The selected CCN-associated VPC is incorrect.       
         The CCN-associated VPC and host address cannot be in the same region (if the network environment of the source database is a VPC in Guangzhou, you cannot select another VPC in Guangzhou as the CCN-associated VPC). The CCN-associated VPC and host address cannot be in the same VPC (if the network environment of the source database is VPC-A, you cannot select VPC-A as the CCN-associated VPC).       
      -  [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.    
 - The Telnet test is passed, but the database connection fails.
     - The migration account is not properly authorized. Authorize it again as instructed in the corresponding scenario in [Migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645) and [data sync](https://intl.cloud.tencent.com/document/product/571/47344).
     - The account or password is incorrect.

 

