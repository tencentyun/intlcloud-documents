After you create a TencentDB for SQL Server instance, you can create different database accounts to allocate and manage databases based on your business needs.
You can create different types of accounts with different permissions for both TencentDB for SQL Server two-node (formerly High Availability/Cluster Edition) and single-node (formerly Basic Edition) instances. This document describes the supported types of accounts and their permissions.

>?TencentDB for SQL Server launched the new database account and permission logic on February 9, 2023. For the mappings between old and new account types and permissions, see [Account Type and Permission Changes](https://www.tencentcloud.com/document/product/238/53972).

## Account types and permissions for two-node (formerly High Availability/Cluster Edition) instances
<table>
<thead><tr><th width=20%>Instance Architecture</th><th width=15%>Account Type</th><th width=35%>Database Permission</th><th>Role Description</th></tr></thead>
<tbody>
<tr>
<td rowspan="5">Two-node (formerly High Availability/Cluster Edition)</td>
<td>Privileged account</td><td>Instance admin account, which has the owner permissions of all databases by default.</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_owner</td></tr>
<tr>
<td rowspan="3">Standard account</td>
<td>Owner</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_owner</td></tr>
<td>Read/Write</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_reader<li>db_writer</td></tr>
<td>Read-only</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_reader</td></tr>
<tr>
<td>Designated account</td><td><li>A designated account can only view and own the specified database. <li>A designated account can be authorized to multiple databases, but a database can be authorized to only one designated account.</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles: <li>db_owner</td></tr>
</tbody></table>

## Account types and permissions for single-node (formerly Basic Edition) instances
<table>
<thead><tr><th width=20%>Instance Architecture</th><th  width=15%>Account Type</th><th width=35%>Database Permission</th><th>Role Description</th></tr></thead>
<tbody>
<td rowspan="6">Single-node (formerly Basic Edition)</td>
<td>Admin account</td><td>Instance admin account, which has the highest-level sysadmin permission and the owner permissions of all databases. <strong>After the admin account is enabled, the product SLA will no longer be guaranteed.</strong></td><td>Server-level roles: <li>sysadmin<br>Database-level roles: <li>db_owner</td></tr>
<td>Privileged account</td><td>It has the owner permissions of all databases by default.</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles: <li>db_owner</td></tr>
<tr>
<td rowspan="3">Standard account</td>
<td>Owner</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_owner</td></tr>
<td>Read/Write</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_reader<li>db_writer</td></tr>
<td>Read-only</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles:<li>db_reader</td></tr>
<tr>
<td>Designated account</td><td><li>A designated account can only view and own the specified database. <li>A designated account can be authorized to multiple databases, but a database can be authorized to only one designated account.</td><td>Server-level roles: <li>securityadmin<li>processadmin<li>dbcreator<br>Database-level roles: <li>db_owner</td></tr>
</tbody></table>
</tbody></table>

