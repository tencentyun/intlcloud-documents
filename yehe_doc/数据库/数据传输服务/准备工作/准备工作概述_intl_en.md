## Overview

When creating a migration, sync, or subscription task, you need to select different access types based on the deployment conditions of your source database. This document describes how to select an access type and prepare accordingly.
![](https://qcloudimg.tencent-cloud.cn/raw/2cbf69b4ea09960c7c1c6c94ce516bc4.png)

## Preparations

<table >
<tr><th width="25%"><strong>Use Case</strong></th><th width="15%"><strong>Access Type</strong></th><th width="60%"><strong>Directions</strong></th></tr>
<tr>
<td>The source database can be accessed through a public IP</td>
<td>Public Network</td>
<td>Add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database to connect the source database and DTS migration instance.</td></tr>
<tr>
<td rowspan="2">The database is in a self-built IDC, which is interconnected with a VPC through VPN or Direct Connect</td>
<td>Direct Connect/VPN Access</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/571/42651">Configure interconnection between the VPN and IDC</a>.</li>
<li>Add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database to connect the source database and DTS migration instance.</li></td></tr>
<tr>
<td>CCN</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/571/42650">Configure VPC-IDC interconnection through CCN</a>.</li>
<li>Add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database.</li></td></tr>
<tr>
<td>The source database is deployed in a CVM instance</td>
<td>Self-Build on CVM</td>
<td>In this scenario, DTS will automatically add the SNAT IP address of the DTS server to a security group rule of the CVM instance, so you don't need to manually add it.</td></tr>
<tr>
<td>The source and target databases are both deployed in Tencent Cloud VPCs.</td>
<td>VPC</td>
<td>Add the SNAT IP address of the DTS server to a security group rule of the source database.<br>The data sync feature supports the VPC access type. To use it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</td></tr>
<tr>
<td>The source database is a TencentDB database</td>
<td>Database</td>
<td>Add the SNAT IP address of the DTS server to a security group rule of the source database.</li></td></tr>
</table>

For a third-party cloud database, you can select **Public Network** generally as the **access type** or select **VPC Access**, **Direct Connect**, or **CCN** based on your actual network conditions.
