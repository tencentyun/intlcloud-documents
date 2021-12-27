## Overview
CCN can interconnect a VPC with another VPC or a local IDC. To use CCN access, you must establish cross-VPC and VPC-IDC interconnections through CCN in advance.

In this scenario, you have used CCN to interconnect the following three networks: vpc-Guangzhou, vpc-Nanjing, and vpc-Shanghai, and plan to migrate a database in the Guangzhou region to the target database. vpc-Nanjing or vpc-Shanghai is selected as the VPC associated with CCN.

<img src="https://qcloudimg.tencent-cloud.cn/raw/e1897064f911913b554bbafcd1cb45be.png" style="zoom:67%;" />

## Directions
Establish interconnections as instructed in [Network Instance Interconnection in One Account](https://intl.cloud.tencent.com/document/product/1003/31986).

> ?CCN only provides bandwidth below 10 Kbps between all regions free of charge. However, DTS requires a higher bandwidth. Therefore, bandwidth configuration in the link is required.

## Subsequent Steps
1. On the [DTS task page](https://console.cloud.tencent.com/dts/migration), select **CCN**.
<table>
<thead><tr><th><strong>Parameter</strong></th><th><strong>Description</strong></th><th><strong>Sample Value</strong></th></tr></thead>
<tbody><tr>
<td>VPC-Based CCN Instance</td><td>CCN instance name.</td><td>ccn6-xxxx7d</td></tr>
<tr>
<td>CCN-Associated VPC</td>
<td>Select a VPC whose name and region are different from those of the VPC of the source database. For example, if you use a database in the Guangzhou region as the source database, you should select **vpc-Nanjing** or **vpc-Shanghai** as the **CCN-associated VPC**. Here, **vpc-Nanjing** is selected.</td>
<td>vpc-Nanjing</td></tr>
<tr>
<td>Subnet</td>
<td>Name of the subnet of the selected VPC.<br>If you cannot pull the subnet, there may be a problem with your account. The account of the CCN-associated VPC must be the same as the migration account.<br>For example, to migrate a database under account A to account B, you should use account B to create a task. Therefore, the CCN-associated VPC must be under account B.</td>
<td>vpc-Nanjing-subnet</td></tr>
<tr>
<td>Host Address</td><td>IP address of the source database server.</td><td>172.16.0.0</td></tr>
<tr>
<td>Port</td>
<td>Port used by the source database. Below are the default ports for common databases (if they are modified, enter the actual ports): <ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
</tbody></table>

2. Click **Test Connectivity**. If the test fails, troubleshoot as follows:
   - The Telnet test fails.
     In the CCN-associated VPC (vpc-Nanjing in this example), purchase a CVM instance and ping the source database server address from it:
     - If the address is unpingable:
      - [The server where the source database resides has a security group or firewall configured](https://intl.cloud.tencent.com/document/product/571/42552).
      - [The SNAT IP address is blocked in the source database](https://intl.cloud.tencent.com/document/product/571/42552).
      - The port settings of the source database are incorrect.
      - Some route tables in the CCN instance are not enabled due to IP range conflicts.
     - If the address is pingable, the routing between the source database and CCN is normal.     
      - The selected CCN-associated VPC is incorrect.       
         The CCN-associated VPC and host address cannot be in the same region (if the network environment of the source database is a VPC in Guangzhou, you cannot select another VPC in Guangzhou as the CCN-associated VPC). The CCN-associated VPC and host address cannot be in the same VPC (if the network environment of the source database is VPC-A, you cannot select VPC-A as the CCN-associated VPC).       
      -  [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.    
 - The Telnet test is passed, but the database connection fails.
     - The migration account is not properly authorized. Authorize it again as instructed in the corresponding scenario in [data migration](https://intl.cloud.tencent.com/document/product/571/42645) and [data sync](https://intl.cloud.tencent.com/document/product/571/42624).
     - The account or password is incorrect.

 

