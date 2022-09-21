## Overview

When creating a migration, sync, or subscription task, you need to select different access types based on the deployment conditions of your source database. This document describes how to select an access type and prepare accordingly.
![](https://qcloudimg.tencent-cloud.cn/raw/2cbf69b4ea09960c7c1c6c94ce516bc4.png)

## Prerequisites

>!Determine the access type in advance. For the same source and target databases, if an access type such as **Public Network** is selected and the connectivity verification is passed, you cannot switch to another access type such as **Direct Connect**; otherwise, an error will be reported during connectivity verification.

- If the source database is an IDC-based self-built database or a third-party cloud database, you can select **Public Network** generally. If you require a higher transfer performance, you can select **VPN Access**, **Direct Connect**, or **CCN** based on your actual network conditions.
- If the source database is a TencentDB instance, select **Database**.
- If the source database is a CVM-based self-built database, select **Self-Build on CVM**.


<table >
<thead><tr><th width="15%"><strong>Access Type</strong></th><th width="25%"><strong>Use Case</strong></th><th width="60%"><strong>Operation Guide</strong></th></tr></thead>
<tr>
<td>Public Network</td>
<td><li>The source database can be accessed through a public IP.</li><li>The public network option cannot guarantee the transfer bandwidth and is applicable to scenarios with low requirements for the transfer performance.</li></td>
<td>Manually add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a> to connect the source database and DTS instance.</td></tr>
<tr>
<td>Direct Connect/VPN Access</td>
<td><ul><li>The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a> or <a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a>.</li><li>The network bandwidth of Direct Connect is guaranteed.</li></ul></td>
<td><ul><li>Configure VPN-IDC interconnection as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/42651">Direct Connect or VPN Access: Configuring VPN-IDC Interconnection</a>.</li>
<li>Manually add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a> to connect the source database and DTS instance.</li></ul></td></tr>
<tr>
<td>CCN</td>
<td>The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>.</td>
<td><ul><li>Configure VPC-IDC interconnection through CCN as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/42650">CCN Access: Configuring VPC-IDC Interconnection Through CCN</a>.</li>
<li>Manually add the SNAT IP of the DTS server to the allowlist (generally the firewall) of the self-built database as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>.</li></ul></td></tr>
<tr>
<td>Self-Build on CVM</td>
<td>The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</td>
<td>Manually add the SNAT IP of the DTS server to the security group of the CVM instance as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a> to connect the source database and DTS instance.</td></tr>
<tr>
<td>VPC</td>
<td>The source and target databases are both deployed in Tencent Cloud VPCs.</td>
<td>Manually add the SNAT IP address of the DTS server to the security group of the source database as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>. <br>To use the VPC access type, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</td></tr>
<tr>
<td>Database</td>
<td>The source database is a TencentDB instance.</td>
<td><ul><li>If the source database is a TencentDB for MySQL, TencentDB for PostgreSQL, TDSQL-C for PostgreSQL, TDSQL for TDStore, TDSQL for PostgreSQL, or TDSQL-A for PostgreSQL instance, DTS will automatically add the SNAT IP address of the DTS server to the security group rule of the source database.</li><li>For other database types, you need to do so manually as instructed in <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>.</li></ul></td></tr>
</table>

> ? 
> - Manually or automatically adding the SNAT IP address of the DTS server to the security group or allowlist of the source database may cause certain security risks to the source database. Therefore, you should enhance security protection measures when performing such operations; for example, you can standardize account password management, require authentication for API communication, and restrict unnecessary IP ranges. By using DTS, you acknowledge the existence of risks. If you have high security requirements, we recommend you use Direct Connect, VPN, or VPC for access.
> - After using DTS, we recommend you delete the DTS IP address from the security group or firewall promptly.

