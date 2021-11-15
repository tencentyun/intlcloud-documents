A TencentDB instance is a standalone database environment running in Tencent Cloud. It includes multiple databases created by users and can be accessed using the same tools and applications as those for a standalone database instance.

TencentDB for PostgreSQL supports the following types of instances:
<table>
<thead><tr><th>Instance Type</th><th width="20%">Definition</th><th width="15%">Architecture</th><th>Visible in the Instance List</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Primary instance</td>
<td>An instance that can be read from and written to</td>
<td>High-availability edition</td>
<td>Yes</td>
<td>The primary instance can associate with read-only replicas to realize read/write separation.</td>
</tr>
<tr>
<td>Read-only replica</td>
<td>An instance that can only be read from</td>
<td>Single-node read-only</td>
<td>Yes</td>
<td><li>A read-only replica cannot exist on its own. Instead, it must be affiliated to a primary instance. Its data comes solely from syncing with the primary instance, and it must reside in the same region as the primary instance.<li>By default, up to six read-only replicas can be created for a primary instance. To create more than six read-only replicas, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
</tbody></table>

### Reference
- For more information on the creation of and notes on the read-only replicas, please see [Creating Read-only Replicas](https://intl.cloud.tencent.com/document/product/409/39545).
- For more information on how to create and configure a read-only replica group (RO group), please see [Managing RO Groups](https://intl.cloud.tencent.com/document/product/409/39546).
